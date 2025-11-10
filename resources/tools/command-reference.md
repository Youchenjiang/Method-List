# 電腦指令參考

本文件收錄常用的命令列指令，包含 CMD、PowerShell、Anaconda、Git 等工具的實用指令。

## 📋 目錄

- [CMD 指令](#cmd-指令)
- [PowerShell 指令](#powershell-指令)
- [Anaconda 套件管理](#anaconda-套件管理)
- [開發工具 CLI](#開發工具-cli)

---

## CMD 指令

### CMD更改資料檔名

`ren *.doc *.java` (將所有doc檔改成java檔)  
`FOR %a in (109*.*) DO REN "%~a" "0%~nxa"` (將所有109開頭檔檔名加上0)

### IP位置查詢

`nslookup + 網址`

### 查詢本機 ARP 快取

`arp -a`

### 網路無法連線

參考: [修復 Windows 10 WiFi 連線問題](https://www.mytechgirl.com/tw/windows/fix-windows-10-wifi-can-not-connect-mtg6688.html)

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

### 自動修復系統功能

```cmd
Dism /Online /Cleanup-Image /CheckHealth
Dism /Online /Cleanup-Image /ScanHealth
Dism /Online /Cleanup-Image /RestoreHealth
sfc /scannow
```

### 開啟任務管理員

`taskmgr`

---

## PowerShell 指令

### PowerShell更改資料檔名

```powershell
Get-ChildItem -Path $directory -Filter "[懷舊與回憶]*.*" | Rename-Item -NewName {"[懷舊]" + ($_.BaseName -replace "^\[懷舊與回憶\]", "") +$_.Extension}
```

將所有[懷舊與回憶]開頭檔檔名將[懷舊與回憶]改為[懷舊]

### 下載最新版的 PowerShell

```powershell
winget search Microsoft.PowerShell
winget install --id Microsoft.Powershell.Preview --source winget
```

### 為目前的 PowerShell 提升至管理員權限

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

### 關閉特定程式

```powershell
# 查找佔用特定端口的程式
PS> netstat -ano | findstr :5173
  TCP    [::1]:5173             [::]:0                 LISTENING       16532
  TCP    [::1]:5173             [::1]:54831            ESTABLISHED     16532
  TCP    [::1]:54831            [::1]:5173             ESTABLISHED     22872

# 終止該程式
PS> taskkill /F /PID 16532
成功: 處理程序 PID 16532 已經終止了。
```

### 激活 Office

使用 [Microsoft Activation Scripts](https://massgrave.dev/):

```powershell
irm https://get.activated.win | iex
```

確認腳本內容-1:

```powershell
irm https://get.activated.win -OutFile .\check-script.ps1
```

確認腳本內容-2:

```powershell
irm 'https://raw.githubusercontent.com/massgravel/Microsoft-Activation-Scripts/ab6b572af940fa0ea4255b327eb6f69a274d6725/MAS/All-In-One-Version-KL/MAS_AIO.cmd' -OutFile .\MAS_AIO.cmd
```

### Git 指令

將變更快取結果覆寫至檔案中:

```powershell
git diff --cached > gitDiffCached.txt
```

將最近 14 筆 commit 紀錄（包含所有分支）的圖形化歷史紀錄覆寫至檔案中：

```powershell
git log -n 14 --graph --all > .\last_commit_changes.txt
```

---

## Anaconda 套件管理

### 升級 conda

升級Anaconda前需要先升級conda:

```bash
conda update conda
```

### 升級 Anaconda

```bash
conda update anaconda
```

### 升級 Spyder

```bash
conda update spyder
```

### 升級所有套件

```bash
conda update --all
```

### 安裝套件

```bash
conda install package
```

### 更新套件

```bash
conda update package
```

### 查詢指令說明

使用 `-h` 後綴查詢某個 conda 指令:

```bash
conda update -h
```

---

## 開發工具 CLI

### Revo Dev Cli

#### 查詢版本號

```bash
acli --version
```

#### 授權

```bash
acli rovodev auth login
```

#### 執行

```bash
acli rovodev run
```

### bmad-method

#### 安裝

```bash
npx bmad-method install
```

---

## 使用說明

這些指令可以直接在對應的命令列介面中執行。建議在執行不熟悉的指令前先備份重要資料。

**版本資訊**

- 創建日期: 2025-10-29
- 來源: 從 computer-commands-reference.md 拆分
- 用途: 快速參考常用命令列指令
