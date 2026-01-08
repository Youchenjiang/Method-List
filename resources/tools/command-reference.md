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

## 使用說明

這些指令可以直接在對應的命令列介面 (CMD / PowerShell / Bash) 中執行。建議在執行不熟悉的指令前先備份重要資料。

**版本資訊**
- 創建日期: 2025-10-29
- 來源: 從 computer-commands-reference.md 拆分
- 用途: 快速參考常用命令列指令
