# PDF Standard Encryption 密碼學原理與高速暴力破解技術

[閱讀英文版 / Back to Security Topics](README.md)

---

## 📖 概述

PDF 格式（ISO 32000-1）定義了 **Standard Security Handler**，用於實現 PDF 檔案的權限保護與密碼存取控制。早期 PDF（PDF 1.1 至 1.6）廣泛採用基於 **MD5 + RC4** 的演算法（Revision 2、3 與 4）。

本篇記錄 PDF 標準加密處理器的金鑰衍生（Key Derivation）演算法細節、使用者密碼（User Password）驗證原理，以及如何使用 Python 進行無渲染庫的高速密碼學暴力破解。

---

## 🔑 加密字典參數說明

加密 PDF 的 `/Encrypt` 字典與檔案末端（Trailer）通常包含以下核心欄位：

| 欄位 | 說明 | 格式範例 |
| :--- | :--- | :--- |
| `/Filter` | 安全處理器類型（通常為 `/Standard`） | Name |
| `/V` | 演算法版本（1: 40-bit RC4, 2: 40-128 bit RC4, 4: AES/RC4） | Integer |
| `/R` | Revision 版本（2: 40-bit, 3/4: 128-bit RC4） | Integer |
| `/Length` | 加密金鑰長度（bit，例如 40 或 128） | Integer |
| `/O` | Owner Password Hash（32 位元組） | Hex String |
| `/U` | User Password Hash（32 位元組） | Hex String |
| `/P` | 權限旗標（32-bit signed integer，以 Little-Endian 打包） | Integer |
| `/ID` | 檔案唯一識別碼（位於 Trailer 中，包含兩個 16-byte Hex） | Array |

---

## 🧮 密鑰衍生與驗證演算法 (Revision 2 ~ 4)

### 1. 密碼填充 (Password Padding)
PDF 標準規範密碼必須填充為固定 32 位元組。若密碼長度小於 32，則以固定常數填充：
```python
PADDING = bytes([
    0x28, 0xBF, 0x4E, 0x5E, 0x4E, 0x75, 0x8A, 0x41,
    0x64, 0x00, 0x4E, 0x56, 0xFF, 0xFA, 0x01, 0x08,
    0x2E, 0x2E, 0x00, 0xB6, 0xD0, 0x68, 0x3E, 0x80,
    0x2F, 0x0C, 0xA9, 0xFE, 0x64, 0x53, 0x69, 0x7A,
])
```

### 2. 計算加密金鑰 (Encryption Key Derivation)

1. 取填充後的密碼（32 bytes）
2. 串接 `/O`（32 bytes）
3. 串接 `/P`（4 bytes，Little-Endian signed integer）
4. 串接 `/ID[0]`（第一段 Document ID，16 bytes）
5. 計算 MD5 雜湊：`h = MD5(password_padded + O + P + ID)`
6. **若 Revision $\ge$ 3**：進行 50 次 MD5 迭代雜湊，每次取前 $N$ 個 bytes（$N = Length / 8$）：
   $$\text{for } i \in [0, 49]: \quad h = \text{MD5}(h[:N])$$
7. 取前 $N$ 位元組作為檔案主加密金鑰：`key = h[:N]`

### 3. 使用者密碼驗證 (User Password Verification)

#### 【Revision 2 (40-bit RC4)】
- 將固定常數 `PADDING` 使用 `key` 進行 RC4 加密。
- 比對加密結果是否與 `/U` 字典的前 32 位元組完全一致。

#### 【Revision 3 & 4 (128-bit RC4)】
- 先計算初始值：`test = MD5(PADDING + ID)`
- 使用 `key` 對 `test` 進行 RC4 加密。
- 接著進行 19 次連續 RC4 加密，每次的子金鑰為 `key` 與輪次數字 $i$ 的 XOR 結果：
  ```python
  for i in range(1, 20):
      round_key = bytes([b ^ i for b in key])
      test = rc4_encrypt(round_key, test)
  ```
- 比對最終 16 位元組結果是否等於 `/U` 字典的前 16 位元組 (`U[:16]`)。

---

## ⚡ 效能優化與暴力破解加速策略

在進行大量字典檔碰撞時，常見的效能瓶頸包括：

1. **避免使用高階 PDF 解析庫進行迴圈驗證**：
   - `pypdf`、`pdfminer`、`PyMuPDF` 在每次呼叫 `decrypt()` 時會解析整個物件樹，速度通常僅有 100~500 pw/s。
   - **直接實作原生 MD5 + RC4 驗證**：直接比對字串，單核心可達 50,000 ~ 150,000 pw/s。
2. **多行程並行處理 (Multiprocessing with Batched Workers)**：
   - Python 受限於 GIL，純 CPU 密集型計算需使用 `multiprocessing.Pool`。
   - 採用批次派工（例如每批 10,000 組密碼）避免跨行程通訊 IPC 過度開銷。
   - 使用 `multiprocessing.Manager().Event()` 在任一 Worker 找到密碼時即時中斷所有程序。

---

## 🔗 相關工具

- 完整實作程式碼：[Script-List/security/pdf-password-cracker](file:///c:/Users/g1014308/Documents/GitHub/Youchen/Script-List/security/pdf-password-cracker)
