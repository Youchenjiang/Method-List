# 電腦指令參考

本文件收錄常用的命令列指令，依據**功能用途**分類，包含 CMD、PowerShell、Git、Anaconda 等工具的實用指令。

## 📋 目錄

- [電腦指令參考](#電腦指令參考)
  - [📋 目錄](#-目錄)
  - [📁 檔案管理 (File Management)](#-檔案管理-file-management)
    - [批次更名 (Rename)](#批次更名-rename)
    - [合併檔案 (Merge)](#合併檔案-merge)
  - [🌐 網路與連線 (Network & Connectivity)](#-網路與連線-network--connectivity)
    - [狀態查詢](#狀態查詢)
    - [連線修復](#連線修復)
  - [⚙️ 系統管理與維護 (System Management)](#️-系統管理與維護-system-management)
    - [系統修復與優化](#系統修復與優化)
    - [權限與程序管理](#權限與程序管理)
    - [軟體啟用與更新](#軟體啟用與更新)
  - [💻 開發與版控 (Development & Version Control)](#-開發與版控-development--version-control)
    - [Git 版本控制](#git-版本控制)
    - [Anaconda 套件管理](#anaconda-套件管理)
    - [開發工具 CLI](#開發工具-cli)
  - [🔌 API 快速測試 (API Quick Test)](#-api-快速測試-api-quick-test)
  - [使用說明](#使用說明)

---

## 📁 檔案管理 (File Management)

### 批次更名 (Rename)

#### CMD 模式
- `ren *.doc *.java` (將所有 doc 檔改成 java 檔)
- `FOR %a in (109*.*) DO REN "%~a" "0%~nxa"` (將所有 109 開頭檔檔名加上 0)

#### PowerShell 模式
- 將所有 `[懷舊與回憶]` 開頭檔檔名中的 `[懷舊與回憶]` 改為 `[懷舊]`：
```powershell
Get-ChildItem -Path $directory -Filter "[懷舊與回憶]*.*" | Rename-Item -NewName {"[懷舊]" + ($_.BaseName -replace "^\[懷舊與回憶\]", "") +$_.Extension}
```

### 合併檔案 (Merge)

#### 1. 純文字合併 (PowerShell - 免安裝)
僅將文字串接，適合整理筆記：
```powershell
Get-Content *.md | Set-Content merged_all.md
```

#### 2. 轉檔並合併 (Pandoc - 需安裝)
合併並轉換為可閱讀的文件格式 (Word/PDF)：
```bash
pandoc *.md -o merged.docx
pandoc *.md -o merged.pdf
```

---

## 🌐 網路與連線 (Network & Connectivity)

### 狀態查詢

- **IP 位置查詢**: `nslookup + 網址`
- **查詢本機 ARP 快取**: `arp -a`

### 連線修復

#### 修復 Windows 10 WiFi 連線問題
參考: [MyTechGirl 教學](https://www.mytechgirl.com/tw/windows/fix-windows-10-wifi-can-not-connect-mtg6688.html)

```cmd
netsh int ip reset
netsh int tcp set heuristics disabled
netsh int tcp set global autotuninglevel=disabled
netsh int tcp set global rss=enabled
shutdown -restart
ipconfig /release
ipconfig /renew
shutdown -restart
```

---

## ⚙️ 系統管理與維護 (System Management)

### 系統修復與優化

#### 自動修復系統功能 (DISM/SFC)
```cmd
Dism /Online /Cleanup-Image /CheckHealth
Dism /Online /Cleanup-Image /ScanHealth
Dism /Online /Cleanup-Image /RestoreHealth
sfc /scannow
```

### 權限與程序管理

#### 開啟任務管理員
- `taskmgr`

#### 關閉特定程式 (PowerShell)
```powershell
# 1. 查找佔用特定端口的程式 (查詢 :5173)
netstat -ano | findstr :5173

# 2. 終止該程式 (PID 為上一步查到的數字，例如 16532)
taskkill /F /PID 16532
```

#### 為目前的 PowerShell 提升至管理員權限
<details>
<summary>點擊展開詳細腳本</summary>

```powershell
# 指定參數值
$svcName = 'W32Time'
$delay = 5

# 獲取當前目錄
$currentDirectory = Get-Location

# 檢查執行原則並提升權限（若需要）
if (-Not ([Security.Principal.WindowsPrincipal][Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole]"Administrator")) {
    Start-Process pwsh -Verb RunAs -ArgumentList "$PSCommandPath"
} else {
    # 保存當前目錄
    Push-Location $currentDirectory
    # 直接執行腳本內容
    $ErrorActionPreference = 'STOP'
    Stop-Service $svcName
    Start-Sleep -Seconds $delay
    Start-Service $svcName
    Write-Host "$svcName restarted"
    # 恢復到原來的目錄
    Pop-Location
    Write-Host "Returned to $currentDirectory"
}
```
</details>

### 軟體啟用與更新

#### 下載或強制升級 PowerShell (Winget)

```powershell
winget search Microsoft.PowerShell
winget install --id Microsoft.Powershell.Preview --source winget

# 若無法自動升級 (例如版本號不匹配)，可嘗試強制安裝指定版本
winget source update
winget install --id Microsoft.PowerShell.Preview --version <Version> --force
```

#### 激活 Office (MAS)
使用 [Microsoft Activation Scripts](https://massgrave.dev/):
```powershell
irm https://get.activated.win | iex
```

---

## 💻 開發與版控 (Development & Version Control)

### Git 版本控制

- **將變更快取結果覆寫至檔案中**:
  ```powershell
  git diff --cached > gitDiffCached.txt
  ```

- **匯出最近 14 筆 Commit 紀錄**:
  ```powershell
  git log -n 14 --graph --all > .\last_commit_changes.txt
  ```

- **專案 Commit 格式校驗 (Git commit-msg Hook)**:
  為了確保開發團隊與 AI 協同代理程式 (Agent) 均能遵守 Conventional Commits 與「分批且列點說明」的規範，我們在專案中使用了 Git `commit-msg` Hook。此機制會在執行 `git commit` 時自動驗證您的提交訊息是否符合規範，若不符則會自動阻擋 (Block)。

  > [!NOTE]
  > **校驗規則概要：**
  > 1. **標頭 (Header)**：必須符合 `type(scope): subject` 或 `type: subject` 格式。支援的類型包含 `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`。
  > 2. **內文 (Body)**：必須以英文的數字列點（以 `1. ` 為起點的列表）詳細說明變更內容，忽略註解行（以 `#` 開頭的行）。

  #### ⚙️ 部署與設定方法
  請在您**需要啟用校驗的 Git 專案根目錄**下，依據您所使用的終端機環境選擇以下對應指令複製並執行：

  ##### 1. Bash / Git Bash 環境
  複製並執行以下 Bash 指令：
  ```bash
  # 1. 確保 hooks 目錄存在
  mkdir -p .git/hooks

  # 2. 寫入並啟用 commit-msg hook
  cat << 'EOF' > .git/hooks/commit-msg
  #!/bin/sh

  # 取得 Commit 訊息暫存檔路徑
  commit_msg_file="$1"

  # 讀取首行標頭
  header=$(head -n 1 "$commit_msg_file")

  # 1. 驗證標頭是否符合 Conventional Commits
  if ! echo "$header" | grep -qE "^(feat|fix|docs|style|refactor|test|chore)(\([^)]+\))?: .+$"; then
    echo "========================================= [COMMIT BLOCKED] ========================================="
    echo "ERROR: Invalid commit message header format."
    echo "Header must follow Conventional Commits: 'type(scope): subject' or 'type: subject'"
    echo "Valid types: feat, fix, docs, style, refactor, test, chore"
    echo "Given header: '$header'"
    echo "===================================================================================================="
    exit 1
  fi

  # 2. 驗證內文是否包含以 '1. ' 開始的英文數字列點
  # 過濾以 # 開頭的註解，並跳過首行標頭進行檢查
  if ! grep -vE "^#" "$commit_msg_file" | tail -n +2 | grep -qE "^\s*1[\.\)]\s+"; then
    echo "========================================= [COMMIT BLOCKED] ========================================="
    echo "ERROR: Commit message body must contain a numbered list in English starting with '1. '"
    echo "Example:"
    echo "  feat(scraper): add scraping functionality"
    echo "  "
    echo "  1. Introduce fetchUrl for HTTP GET requests."
    echo "  2. Implement HTML parser."
    echo "===================================================================================================="
    exit 1
  fi

  exit 0
  EOF

  # 3. 賦予可執行權限
  chmod +x .git/hooks/commit-msg
  echo "✓ 已成功為此專案啟用 Commit 格式校驗 Hook"
  ```

  ##### 2. PowerShell 環境 (Windows 推薦)
  如果使用 Windows PowerShell，請複製並執行以下指令：
  ```powershell
  # 1. 確保目前目錄下的 .git/hooks 資料夾存在
  New-Item -ItemType Directory -Force -Path ".\.git\hooks"

  # 2. 定義 Hook 腳本內容
  $hookContent = @'
  #!/bin/sh

  # 取得 Commit 訊息暫存檔路徑
  commit_msg_file="$1"

  # 讀取首行標頭
  header=$(head -n 1 "$commit_msg_file")

  # 1. 驗證標頭是否符合 Conventional Commits
  if ! echo "$header" | grep -qE "^(feat|fix|docs|style|refactor|test|chore)(\([^)]+\))?: .+$"; then
     echo "========================================= [COMMIT BLOCKED] ========================================="
     echo "ERROR: Invalid commit message header format."        
     echo "Header must follow Conventional Commits: 'type(scope): subject' or 'type: subject'"
     echo "Valid types: feat, fix, docs, style, refactor, test, chore"
     echo "Given header: '$header'"
     echo "===================================================================================================="
     exit 1
  fi

  # 2. 驗證內文是否包含以 '1. ' 開始的英文數字列點
  # 過濾以 # 開溫的註解，並跳過首行標頭進行檢查
  if ! grep -vE "^#" "$commit_msg_file" | tail -n +2 | grep -qE "^\s*1[\.\)]\s+"; then
     echo "========================================= [COMMIT BLOCKED] ========================================="
     echo "ERROR: Commit message body must contain a numbered list in English starting with '1. '"
     echo "Example:"
     echo "  feat(scraper): add scraping functionality"
     echo "  "
     echo "  1. Introduce fetchUrl for HTTP GET requests."      
     echo "  2. Implement HTML parser."
     echo "===================================================================================================="
     exit 1
  fi

  exit 0
  '@

  # 3. 寫入檔案（使用 PowerShell 原生路徑解析，並強制無 BOM 的 UTF-8 編碼）
  $hookContent | Out-File -FilePath ".\.git\hooks\commit-msg" -Encoding utf8NoBOM

  # 4. 讓 Git 標記該檔案為可執行檔
  git update-index --chmod=+x .\.git\hooks\commit-msg

  # 5. 輸出成功訊息
  Write-Host "✓ 已成功為此專案啟用 Commit 格式校驗 Hook！" -ForegroundColor Green

  # 6. (選用) 驗證 Hook 檔案內容
  Get-Content .\.git\hooks\commit-msg
  ```

  > [!TIP]
  > **如何暫時繞過校驗？**
  > 如果在特殊緊急情況下，您需要強制提交而不進行格式檢查，可以在 `git commit` 時加上 `--no-verify` 參數：
  > ```bash
  > git commit -m "temp bypass commit" --no-verify
  > ```

### Anaconda 套件管理

| 動作              | 指令                    | 備註                     |
| ----------------- | ----------------------- | ------------------------ |
| **升級 Conda**    | `conda update conda`    | 升級 Anaconda 前需先執行 |
| **升級 Anaconda** | `conda update anaconda` |                          |
| **升級 Spyder**   | `conda update spyder`   |                          |
| **升級所有套件**  | `conda update --all`    |                          |
| **安裝套件**      | `conda install package` |                          |
| **更新套件**      | `conda update package`  |                          |
| **查詢說明**      | `conda update -h`       | 使用 `-h` 查詢用法       |

### 開發工具 CLI

#### Revo Dev Cli
- `acli --version` (查詢版本)
- `acli rovodev auth login` (授權)
- `acli rovodev run` (執行)

#### bmad-method
- `npx bmad-method install` (安裝)

---

## 🔌 API 快速測試 (API Quick Test)

### LLM API (OpenAI-compatible)

使用 `curl` 快速測試 LLM API 是否可用：

```powershell
curl.exe -i https://api.example.com/v1/chat/completions `
  -H "Content-Type: application/json" `
  -H "Authorization: Bearer YOUR_API_KEY" `
  -d '{ "model": "model-name", "messages": [{"role": "user", "content": "hi"}] }'
```

| 參數 | 說明 |
| :--- | :--- |
| `-i` | 顯示回應 Header（含 HTTP 狀態碼） |
| `-H "Content-Type: application/json"` | 指定請求格式為 JSON |
| `-H "Authorization: Bearer ..."` | API 金鑰認證 |
| `-d '{...}'` | POST 請求 body |

#### 常見 LLM API 端點

| 服務 | 端點 | 模型範例 |
| :--- | :--- | :--- |
| **SiliconFlow** | `https://api.siliconflow.cn/v1/chat/completions` | `Qwen/Qwen3.5-9B` |
| **OpenAI** | `https://api.openai.com/v1/chat/completions` | `gpt-4o` |
| **Groq** | `https://api.groq.com/openai/v1/chat/completions` | `llama-3.3-70b-versatile` |
| **OpenRouter** | `https://openrouter.ai/api/v1/chat/completions` | `anthropic/claude-sonnet-4` |

> [!TIP]
> **Windows PowerShell 注意事項**
> - 使用 `curl.exe`（而非 `curl`），避免 PowerShell 內建别名的問題
> - 多行指令使用反引號 `` ` `` 換行（而非 `\`）
> - 也可使用 `Invoke-RestMethod` 取代 curl：
>   ```powershell
>   Invoke-RestMethod -Uri "https://api.example.com/v1/chat/completions" `
>     -Method POST `
>     -Headers @{"Authorization"="Bearer YOUR_API_KEY"; "Content-Type"="application/json"} `
>     -Body '{"model":"model-name","messages":[{"role":"user","content":"hi"}]}'
>   ```

---

## 使用說明

這些指令可以直接在對應的命令列介面 (CMD / PowerShell / Bash) 中執行。建議在執行不熟悉的指令前先備份重要資料。

**版本資訊**
- 創建日期: 2025-10-29
- 來源: 從 computer-commands-reference.md 拆分
- 用途: 快速參考常用命令列指令
