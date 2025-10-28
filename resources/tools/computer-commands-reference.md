# 電腦指令統整

- [電腦指令統整](#電腦指令統整)
  - [內建指令](#內建指令)
    - [CMD](#cmd)
      - [更改資料檔名](#更改資料檔名)
      - [IP位置查詢](#ip位置查詢)
      - [查詢本機 ARP 快取](#查詢本機-arp-快取)
      - [網路無法連線(參考)](#網路無法連線參考)
      - [自動修復系統功能](#自動修復系統功能)
      - [開啟任務管理員](#開啟任務管理員)
    - [PowerShell](#powershell)
      - [更改資料檔名](#更改資料檔名-1)
      - [下載最新版的Powershell](#下載最新版的powershell)
      - [為目前的Powershell提升至管理員權限](#為目前的powershell提升至管理員權限)
- [指定參數值](#指定參數值)
- [獲取當前目錄](#獲取當前目錄)
- [檢查執行原則並提升權限（若需要）](#檢查執行原則並提升權限若需要)
      - [關閉特定程式](#關閉特定程式)
      - [激活Office](#激活office)
      - [將這次變更快取結果覆寫至檔案中](#將這次變更快取結果覆寫至檔案中)
    - [Anaconda](#anaconda)
      - [conda(升級Anaconda前需要先升級conda)](#conda升級anaconda前需要先升級conda)
      - [anaconda](#anaconda-1)
      - [spyder](#spyder)
      - [所有套件](#所有套件)
      - [安裝套件](#安裝套件)
      - [更新套件](#更新套件)
      - [查詢某個conda指令使用-h後綴](#查詢某個conda指令使用-h後綴)
    - [Revo Dev Cli](#revo-dev-cli)
      - [查詢版本號](#查詢版本號)
      - [授權](#授權)
      - [執行](#執行)
    - [bmad-method](#bmad-method)
      - [install](#install)
  - [搜尋工具](#搜尋工具)
    - [系統資訊](#系統資訊)
    - [電腦管理](#電腦管理)
    - [裝置管理員](#裝置管理員)
  - [瀏覽器功能](#瀏覽器功能)
    - [網頁文字高亮](#網頁文字高亮)
  - [快捷鍵](#快捷鍵)
    - [安全性選項](#安全性選項)
    - [即時系統監測](#即時系統監測)
    - [完全截圖](#完全截圖)
    - [部分擷圖](#部分擷圖)
  - [軟體操作](#軟體操作)
    - [VScode](#vscode)
    - [SQL 語法](#sql-語法)
  - [Chrome-Flags](#chrome-flags)
    - [Auto Dark Mode for Web Contents - 【Enable】](#auto-dark-mode-for-web-contents---enable)
    - [Tab Scrolling - 【Enabled - tabs shrink to a large width】](#tab-scrolling---enabled---tabs-shrink-to-a-large-width)
    - [Reading Mode Read Aloud - 【Enable】](#reading-mode-read-aloud---enable)
    - [Reading Mode Read Aloud Phrase Highlighting - 【Enable】](#reading-mode-read-aloud-phrase-highlighting---enable)
    - [Link Preview - 【Enable】](#link-preview---enable)
    - [Parallel downloading - 【Enable】](#parallel-downloading---enable)
  - [Excel](#excel)
    - [常用函數](#常用函數)
      - [計算工作時間](#計算工作時間)
      - [自動計算出勤天數](#自動計算出勤天數)
      - [自動計算工時](#自動計算工時)
      - [自動計算加班工時](#自動計算加班工時)
      - [自動計算週六日上班工時](#自動計算週六日上班工時)
      - [其他](#其他)
    - [常用快捷鍵](#常用快捷鍵)

## 內建指令

### CMD

#### 更改資料檔名

`ren *.doc *.java` (將所有doc檔改成java檔)  
`FOR %a in (109*.*) DO REN "%~a" "0%~nxa"` (將所有109開頭檔檔名加上0)

#### IP位置查詢

`nslookup + 網址`

#### 查詢本機 ARP 快取

`arp -a`

#### 網路無法連線[(參考)](https://www.mytechgirl.com/tw/windows/fix-windows-10-wifi-can-not-connect-mtg6688.html)

`netsh int ip reset`  
`netsh int tcp set heuristics disabled`  
`netsh int tcp set global autotuninglevel=disabled`  
`netsh int tcp set global rss=enabled`  
`shutdown -restart`  
`ipconfig /release`  
`ipconfig /renew`  
`shutdown -restart`

#### 自動修復系統功能

`Dism /Online /Cleanup-Image /CheckHealth`  
`Dism /Online /Cleanup-Image /ScanHealth`  
`Dism /Online /Cleanup-Image /RestoreHealth`  
`sfc /scannow`

#### 開啟任務管理員

`taskmgr`

### PowerShell

#### 更改資料檔名

`Get-ChildItem -Path $directory -Filter "[懷舊與回憶]*.*" | Rename-Item -NewName {"[懷舊]" + ($_.BaseName -replace "^\[懷舊與回憶\]", "") +$_.Extension}` (將所有[懷舊與回憶]開頭檔檔名將[懷舊與回憶]改為[懷舊])

#### 下載最新版的Powershell

`winget search Microsoft.PowerShell`  
`winget install --id Microsoft.Powershell.Preview --source winget`

#### 為目前的Powershell提升至管理員權限

# 指定參數值  
`$svcName = 'W32Time'`  
`$delay = 5`

# 獲取當前目錄  
`$currentDirectory = Get-Location`  
# 檢查執行原則並提升權限（若需要）  
`if (-Not ([Security.Principal.WindowsPrincipal][Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole]"Administrator")) {`  
    `Start-Process pwsh -Verb RunAs -ArgumentList "$PSCommandPath"`  
`} else {`  
    # 保存當前目錄  
    `Push-Location $currentDirectory`  
    # 直接執行腳本內容  
    `$ErrorActionPreference = 'STOP'`  
    `Stop-Service $svcName`  
    `Start-Sleep -Seconds $delay`  
    `Start-Service $svcName`  
    `Write-Host "$svcName restarted"`  
    # 恢復到原來的目錄  
    `Pop-Location`  
    `Write-Host "Returned to $currentDirectory"`  
`}`

#### 關閉特定程式

`PS C:\Users\jerry.jiang38\Documents\Project\orange_backend> netstat -ano | findstr :5173`  
  `TCP    [::1]:5173             [::]:0                 LISTENING       16532`  
  `TCP    [::1]:5173             [::1]:54831            ESTABLISHED     16532`  
  `TCP    [::1]:54831            [::1]:5173             ESTABLISHED     22872`  
`PS C:\Users\jerry.jiang38\Documents\Project\orange_backend> taskkill /F /PID 16532`        
成功: 處理程序 PID 16532 已經終止了。

#### 激活Office

[Microsoft Activation Scripts](https://massgrave.dev/):

`irm https://get.activated.win | iex`

確認腳本內容-1:

`irm https://get.activated.win -OutFile .\check-script.ps1`

確認腳本內容-2:

`irm 'https://raw.githubusercontent.com/massgravel/Microsoft-Activation-Scripts/ab6b572af940fa0ea4255b327eb6f69a274d6725/MAS/All-In-One-Version-KL/MAS_AIO.cmd' -OutFile .\MAS_AIO.cmd`


#### 將這次變更快取結果覆寫至檔案中

`git diff --cached > gitDiffCached.txt`

### Anaconda

#### conda(升級Anaconda前需要先升級conda)

`conda update conda`

#### anaconda

`conda update anaconda`

#### spyder

`conda update spyder`

#### 所有套件

`conda update --all`

#### 安裝套件

`conda install package`

#### 更新套件

`conda update package`

#### 查詢某個conda指令使用-h後綴

`conda update -h`

### Revo Dev Cli

#### 查詢版本號

`acli --version`

#### 授權

`acli rovodev auth login`

#### 執行

`acli rovodev run`

### bmad-method

#### install

`npx bmad-method install`

## 搜尋工具

### 系統資訊

查詢bios版本與日期

### 電腦管理

磁碟資訊

### 裝置管理員

管理驅動程式

## 瀏覽器功能

### 網頁文字高亮

在網址後加上 `#:~:text=關鍵字` 可將搜尋結果高亮顯示  
範例：`https://example.com#:~:text=允許存取檔案網址`  
功能：自動高亮頁面中的「允許存取檔案網址」文字

## 快捷鍵

### 安全性選項

ctrl + alt + .

### 即時系統監測

[Windows 鍵]+ G

### 完全截圖

[Windows 鍵]+ alt + prtscreen

### 部分擷圖

[Windows 鍵]+ Shift + S

## 軟體操作

### VScode

VS Code進行列選擇：alt+shift+滑鼠左鍵拖曳

### SQL 語法

設定MySQL欄位只能輸入0和1  
`USE orange_dev;`  
`ALTER TABLE Employees`  
`ADD CONSTRAINT chk_permission CHECK (Permission IN (0, 1));`

## Chrome-Flags

### Auto Dark Mode for Web Contents - 【Enable】

### Tab Scrolling - 【Enabled - tabs shrink to a large width】

### Reading Mode Read Aloud - 【Enable】

### Reading Mode Read Aloud Phrase Highlighting - 【Enable】

### Link Preview - 【Enable】

### Parallel downloading - 【Enable】

## Excel

### 常用函數

#### 計算工作時間

簽到/退的時間計算工作小時數，公式為：`=TEXT(H9-G9,h:mm)`

#### 自動計算出勤天數

在考勤區域輸入員工考勤情況，輸入countif函數計算考勤天數

#### 自動計算工時

在單元格中輸入函數的計算公式:`=hour(b2-a2)+minute(b2-a2)/60-C2`，然後生成函數計算結果。使用SUMPRODUCT函數來批量生成公式計算結果

#### 自動計算加班工時

在單元格中將加班和加班時間分開，在單元格輸入`=int((hour(c2-b2)*60+minute(c2-b2))/30)/2`

#### 自動計算週六日上班工時

weekday函數來判斷某一天是星期六還是星期日，然後使用sumproduct函數來計算這些天的工時

#### 其他

SUM：求和`=SUM(A1:A5)`  
AVERAGE：平均值`=AVERAGE(A1:A5)`  
IF：條件判斷`=IF(A1>5,“≥5","≤5")`  
VLOOKUP：垂直查找`=VLOOKUP(A1,A2:B6,2,FALSE)`  
DATE：創建日期`=DATE(2024,1,10)`

### 常用快捷鍵

Alt+= 自動求和  
Alt+Enter 單元格內換行  
Ctrl+U 字體加下滑線  
Ctrl+5 設置文字刪除線  
Ctrl+Shift+~ 設置常規數字格式
