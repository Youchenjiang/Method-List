# 🚩 CTF 奪旗賽技術與賽制指南 (CTF Technical & Methodology Guide)

> 📌 **來源聲明**：本指南競賽方法論與領域分類整理自 [飛飛的資安學習筆記 - 資安新手 CTF 入門指南](https://feifei.tw/ctf-beginners-guide-resources/)，經提煉與結構化，專為 CTF 賽制與競賽技術速查使用。
> 🔗 **學習平台與靶場清單**：關於 TryHackMe, picoCTF, HTB, DVWA 等練習平台，請參閱 [網安學習平台與實務靶場對照表](cybersecurity-labs-and-platforms.md)。

---

## 📋 1. CTF 6 大領域分類與技能卡

| 領域標籤 | 英文名稱 | 核心測試目標 | 必備基礎知識與解題重點 |
| :--- | :--- | :--- | :--- |
| **Pwn** | Binary Exploitation | 程式弱點利用、記憶體控制、取得 Shell/Root 權限 | C/C++、組合語言 (x86/x64)、記憶體配置 (Stack/Heap)、ROP 鏈構造 |
| **Reverse** | Reverse Engineering | 逆向工程、分析執行檔邏輯、推導保護機制與演算法 | 組合語言、靜態/動態分析、控制流程分析、邏輯破譯 |
| **Web** | Web Exploitation | 網站漏洞滲透（SQLi, XSS, CSRF, SSRF, RCE, 序列化） | HTTP 協定、PHP/Python/Node.js、資料庫語法、前端/後端漏洞利用 |
| **Forensics**| Digital Forensics | 數位鑑識、記憶體 Dump 分析、封包軌跡與檔案碎片提取 | 網路封包 (pcap)、檔頭 (Magic Bytes)、磁碟鏡像、記憶體鑑識 |
| **Crypto** | Cryptography | 密碼學破譯、數學推導、演算法實作瑕疵破解 | 數論 (RSA, ECC)、對稱/非對稱加密、雜湊演算法、數學推導 |
| **Misc** | Miscellaneous | 雜項（OSINT 公開情報搜集、隱寫術 Steganography、編碼） | Base64/Hex 解碼、圖片/音訊隱寫分析、詮釋資料 (Exif) 提取 |

---

## 🏆 2. 8 大 CTF 賽制模式對照表

| 賽制模式 | 運作機制 | 攻防焦點 | 競賽難度與特色 |
| :--- | :--- | :--- | :--- |
| **Jeopardy (解題型)** | 各題型獨立，找到 Flag 提交計分 | 專注獨立題目分析與解題能力 | **初學者友善**；獨立解題、時間累積得分 |
| **Attack-Defense (攻防型)** | 攻擊對方伺服器 + 防禦自己服務 | 攻防並重、即時 Patch 漏洞與日誌監控 | **高**；團隊作戰、即時回應攻擊 |
| **King of the Hill (KoTH)** | 搶佔主機控制權並保持維持時間 | 快速攻陷 + 系統加固與排他防禦 | **高**；依控制時間計分，強調防禦與加固 |
| **Boot2Root (主機滲透)** | 攻入目標虛擬機取得 Root 權限 | 完整滲透測試流程 (Recon ➔ PrivEsc) | **中 ~ 高**；資訊搜集到權限提升完整鏈條 |
| **Real-World Simulation** | 模擬企業多層網路/工控/雲端攻防 | 企業級真實場景與團隊協同作戰 | **高**；貼近真實企業網路架構 |
| **AI / 自動化型** | 開發自動化 Agent/工具挖掘與修復漏洞 | 演算法、LLM 應用與程式自動化 | **高**；高度依賴編程與演算法設計 |
| **Education (教育型)** | 附帶 Hints 與教學指引之循序漸進題目 | 引導學習、建構基礎安全觀念 | **低 ~ 中**；教學導向，注重觀念建構 |
| **Red vs Blue (企業實戰)** | 紅隊 (攻擊) vs 藍隊 (事件應變) | 事件應變 (IR)、威脅偵測與企業防衛 | **中 ~ 高**；模擬企業內網真實攻防演練 |

---

## 🧰 3. CTF 實用工具箱與命令速查

### 基礎 CLI 命令速查

```bash
# 1. 檔案類型與基本資訊識別
file target_file                # 辨識檔案格式 (ELF, PE, Zip, etc.)
strings target_file | grep -i flag  # 提取可讀字串搜尋 Flag
binwalk -e target_file          # 自動分析與解包隱藏檔案/韌體

# 2. Pwn 二進位安全機制檢查 (需安裝 checksec)
checksec --file=target_bin      # 檢查 NX, ASLR, PIE, Canary 狀態

# 3. 網路互動與連線
nc ip port                      # Netcat 連線至題目伺服器
```

### 各領域常用解析工具

* **Reverse**：Ghidra, IDA Free, radare2, Binary Ninja, x64dbg
* **Pwn**：GDB + pwndbg/peda, pwntools, ROPgadget, one_gadget
* **Web**：Burp Suite, OWASP ZAP, Postman, SQLmap
* **Forensics**：Wireshark, Volatility 3, Autopsy, FTK Imager
* **Crypto / Misc**：CyberChef, Hashcat, John the Ripper, zsteg, Stegsolve

---

## 🏆 4. 全球與台灣知名 CTF 賽事清單

### 國際知名賽事

| 賽事名稱 | 類型 | 難度定位 | 官方連結 |
| :--- | :--- | :--- | :--- |
| **DEF CON CTF** | 團體攻防賽 | 極高 (資安界奧林匹克) | [CTFTime - DEF CON](https://ctftime.org/event/defcon) |
| **Google CTF** | 團體解題+決賽 | 中高 (題目創新具挑戰性) | [Google CTF 官網](https://capturetheflag.withgoogle.com/) |
| **PlaidCTF** | CMU PPP 團體賽 | 中高 (偏實用技術導向) | [CTFTime - PlaidCTF](https://ctftime.org/event/plaidctf) |
| **HITCON CTF** | 國際團體賽 | 高 (台灣 HITCON 主辦頂級賽事) | [CTFTime - HITCON](https://ctftime.org/event/hitcon) |
| **picoCTF** | 個人/團體賽 | 低~中 (CMU 新手入門正式賽) | [picoCTF 官網](https://picoctf.org/) |

### 台灣區域賽事

* **AIS3 EOF CTF**：教育部資安計畫主辦，提供高手預選與高難度 EOF 實體決賽。
* **HITCON CTF**：國際頂級賽事，亦提供本地隊伍競賽切磋。
* **大專院校社群賽**：台大、清大、陽明交大等校內資安社群賽事。

---

## 🗺️ 5. 實戰解題 SOP 與學習心態

```text
[選擇 1~2 個領域] ➔ [基礎題型練習] ➔ [卡關研讀 Writeup]
                                         │
[每週參與線上賽 (CTFTime)] ◄─── [建立個人 Cheatsheet] ◄─┘
```

1. **單點突破**：先專精 Pwn, Reverse, Web, Forensics, Crypto 其中 1~2 個領域，切勿盲目全開。
2. **研讀 Writeup**：卡關時觀看不同戰隊的 Writeup，學習工具用法與解題邏輯。
3. **建立個人 Cheatsheet**：記錄可複用的 Payload、常用命令、解題腳本模組。
