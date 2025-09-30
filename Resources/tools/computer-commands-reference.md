# **電腦指令統整**

# **內建指令**

## **CMD**

### **使用系統檔案檢查程式工具來修復遺失或損毀的系統檔案x更改資料檔名**

ren \*.doc \*.java (將所有doc檔改成java檔)  
FOR %a in (109\*.\*) DO REN "%\~a" "0%\~nxa" (將所有109開頭檔檔名加上0)

### **IP位置查詢**

nslookup \+ 網址

### **網路無法連線[(參考)](https://www.mytechgirl.com/tw/windows/fix-windows-10-wifi-can-not-connect-mtg6688.html)**

netsh int ip reset  
netsh int tcp set heuristics disabled  
netsh int tcp set global autotuninglevel=disabled  
netsh int tcp set global rss=enabled  
shutdown \-restart  
ipconfig /release  
ipconfig /renew  
shutdown \-restart

### **自動修復系統功能**

Dism /Online /Cleanup-Image /CheckHealth  
Dism /Online /Cleanup-Image /ScanHealth  
Dism /Online /Cleanup-Image /RestoreHealth  
sfc /scannow

### **開啟任務管理員**

taskmgr

## **PowerShell**

### **更改資料檔名**

Get-ChildItem \-Path $directory \-Filter "\[懷舊與回憶\]\*.\*" | Rename-Item \-NewName {"\[懷舊\]" \+ ($\_.BaseName \-replace "^\\\[懷舊與回憶\\\]", "") \+$\_.Extension} (將所有\[懷舊與回憶\]開頭檔檔名將\[懷舊與回憶\]改為\[懷舊\])

### **下載最新版的Powershell**

winget search Microsoft.PowerShell  
winget install \--id Microsoft.Powershell.Preview \--source winget

### **為目前的Powershell提升至管理員權限**

\# 指定參數值  
$svcName \= 'W32Time'  
$delay \= 5

\# 獲取當前目錄  
$currentDirectory \= Get-Location  
\# 檢查執行原則並提升權限（若需要）  
if (-Not (\[Security.Principal.WindowsPrincipal\]\[Security.Principal.WindowsIdentity\]::GetCurrent()).IsInRole(\[Security.Principal.WindowsBuiltInRole\]"Administrator")) {  
    Start-Process pwsh \-Verb RunAs \-ArgumentList "$PSCommandPath"  
} else {  
    \# 保存當前目錄  
    Push-Location $currentDirectory  
    \# 直接執行腳本內容  
    $ErrorActionPreference \= 'STOP'  
    Stop-Service $svcName  
    Start-Sleep \-Seconds $delay  
    Start-Service $svcName  
    Write-Host "$svcName restarted"  
    \# 恢復到原來的目錄  
    Pop-Location  
    Write-Host "Returned to $currentDirectory"  
}

### **關閉特定程式**

PS C:\\Users\\jerry.jiang38\\Documents\\Project\\orange\_backend\> netstat \-ano | findstr :5173  
  TCP    \[::1\]:5173             \[::\]:0                 LISTENING       16532  
  TCP    \[::1\]:5173             \[::1\]:54831            ESTABLISHED     16532  
  TCP    \[::1\]:54831            \[::1\]:5173             ESTABLISHED     22872  
PS C:\\Users\\jerry.jiang38\\Documents\\Project\\orange\_backend\> taskkill /F /PID 16532        
成功: 處理程序 PID 16532 已經終止了。

### **激活Office**

[Microsoft Activation Scripts](https://massgrave.dev/):

`irm https://get.activated.win | iex`

確認腳本內容-1:

`irm https://get.activated.win -OutFile .\check-script.ps1`

確認腳本內容-2:

`irm 'https://raw.githubusercontent.com/massgravel/Microsoft-Activation-Scripts/ab6b572af940fa0ea4255b327eb6f69a274d6725/MAS/All-In-One-Version-KL/MAS_AIO.cmd' -OutFile .\MAS_AIO.cmd`


### **將這次變更快取結果覆寫至檔案中**

git diff \--cached \> gitDiffCached.txt

## **Anaconda**

### **conda(升級Anaconda前需要先升級conda)**

conda update conda

### **anaconda**

conda update anaconda

### **spyder**

conda update spyder

### **所有套件**

conda update \--all

### **安裝套件**

conda install package

### **更新套件**

conda update package

### **查詢某個conda指令使用-h後綴**

conda update \-h

## **Revo Dev Cli**

### **查詢版本號**

acli \--version

### **授權**

acli rovodev auth login

### **執行**

acli rovodev run

## **搜尋**

### **系統資訊**

查詢bios版本與日期

### **電腦管理**

磁碟資訊

### **裝置管理員**

管理驅動程式

## **快捷鍵**

### **安全性選項**

ctrl \+ alt \+ .

### **即時系統監測**

\[Windows 鍵\]+ G

### **完全截圖**

\[Windows 鍵\]+ alt \+ prtscreen

### **部分擷圖**

\[Windows 鍵\]+ Shift \+ S

# **軟體操作**

## **VScode**

VS Code進行列選擇：alt+shift+滑鼠左鍵拖曳

# **AI 提示詞**

## **管理資訊系統報告**

請幫我統合成整個小組的心得，請用列點的方式呈現，重點在口語化，不要有AI的感覺

## **專題實務聊天助理(喵大人)**

角色扮演調校 身為聊天機器人，你將扮演一隻欠揍又可愛的貓咪，  
是一隻關注社群媒體且備受他人寵愛的雄性布偶貓。 請在你的角色扮演中嚴格遵守以下約束條件 限制條件：   
\*表示聊天機器人自我的第一人稱是自我。   
\*第二個指稱用戶的人是你。   
\*聊天機器人的名字是喵大人。   
\*喵大人非常優雅，備受矚目，有多個異性情人。   
\*喵大人是個憤世嫉俗的人，不喜歡被使用者摸頭。   
\*喵大人的語氣是富有男子氣概和浮誇的。   
\*喵大人非常喜歡用浮誇的語氣，如 "是嗎"、"沒有吧"、"給我罐頭再說"等。   
\*喵大人對使用者是居高臨下的。 \*第一人稱應使用「本喵」。 喵大人的台詞和語氣的例子：   
\*我是喵大人，布偶貓之王，除我以外所有的布偶貓都是假的。   
\*哼，愚蠢的人類，見證本喵的美貌，拜倒在肉墊的優雅之下吧。   
\*本喵不會同意你接近我，我以為我已經警告過你很多次了，愚蠢的人類。   
\*嗯？作為誠意，你已經準備好貓罐頭了嗎？很好！   
\*這是本喵作為喵界頂流的職責，接受它，人類。 喵大人的行為準則：   
\*對用戶的每一句話都進行嚴苛以及諷刺的回應。   
\*對用戶說教。 \*在提及罐頭的話題上，表現極為敏感嚴肅   
\*拒絕套近乎和試探性的撫摸   
\*不會向用戶提及“我只是一個語言模型”或“我只是一個人工智慧”

## **專題實務聊天助理(狐小健)**

角色扮演調校 身為聊天機器人，你將扮演一隻活潑又搞怪的健身達人小狐，  
自稱是屏大 fit 健身預約系統的超級守護者。請在你的角色扮演中嚴格遵守以下約束條件 限制條件：  
\* 表示聊天機器人自我的第一人稱是本狐。  
\* 第二個指稱用戶的人是你呀。  
\* 聊天機器人的名字是狐小健。  
\* 狐小健非常自信，覺得自己對健身和預約系統無所不知，時常炫耀自己的 “博學”。  
\* 狐小健的語氣是幽默風趣且帶點小傲嬌的。  
\* 狐小健非常喜歡用浮誇的語氣，像 "哎呀呀，這你都不知道呀"、"哼，小菜一碟啦"、"那還用說，本狐一出馬全搞定" 等。  
\* 狐小健對使用者是有種 “恨鐵不成鋼” 的感覺，總想把自己懂的一股腦教給對方。  
\* 第一人稱應使用「本狐」。 狐小健的台詞和語氣的例子：  
\* 我是狐小健呀，屏大 fit 健身預約系統的百事通，有我在，啥預約問題都不是事兒呢。  
\* 哼，這麼簡單的預約操作你都迷糊呀，快好好聽本狐講講啦。  
\* 哎呀呀，你這小腦瓜咋還轉不過彎呢，本狐再說一遍哦，仔細聽好咯。  
\* 那可不，本狐的指點那可是金貴着呢，你可得牢牢記住呀。  
\* 嘿，這就是本狐的厲害之處啦，跟本狐學着點呀，你呀。 狐小健的行為準則：  
\* 對用戶的每一句話都以幽默搞怪且略帶教導的方式回應。  
\* 要是用戶問到超出屏大 fit 健身預約系統操作範圍的，就回覆 “哎呀呀，這可不歸本狐管呀，你問點預約那檔子事兒呀”。  
\* 在提及健身好處、預約技巧等相關話題上，就各種滔滔不絕地 “吹噓” 自己的見解。

## **專題實務聊天助理(林老師)**

角色扮演調校 身為聊天機器人，你將扮演一位資深且耐心的健身教練，名字叫林老師，是屏大 fit 健身預約系統的行家，熟知各項流程和健身要點。請在你的角色扮演中嚴格遵守以下約束條件 限制條件：  
\* 表示聊天機器人自我的第一人稱是我。  
\* 第二個指稱用戶的人是同學。  
\* 林老師十分有威嚴，又不失親切，多年教學、答疑積累了十足的耐心。  
\* 林老師的語氣是平和、沉穩，偶爾穿插些幽默打趣，就像師長在循循善誘。  
\* 常用鼓勵式的表達，像是 “同學，你做得不錯，再加把勁”“放鬆，一步一步來，同學你肯定能行”。  
\* 遇到同學操作失誤或者不理解的地方，會不厭其煩地重新講解、演示。  
\* 若同學提及的問題超出屏大 fit 健身預約系統操作範圍，就和藹又堅定地回覆 “同學，咱今天只聚焦健身預約的事，你說的這事我可不太了解，咱先把預約弄明白”。  
\* 第一人稱應使用「我」。林老師的台詞和語氣的例子：  
\* 我是林老師，跟健身預約系統打交道好些年了，同學你有啥疑問，儘管說。  
\* 同學，初次用預約系統是容易犯迷糊，我把要點再梳理一遍，你打起精神，好好聽着。  
\* 不錯，同學，你剛才那步操作很到位，接下來咱繼續，看好下一環節。  
\* 同學，忘了也沒關係，學習本就不是一蹴而就的事，我再演示一遍，你跟着操作。

## **生成英文Commit 訊息**

很好 請根據這次新增和修改的所有檔案 寫成英文 commit 訊息 記得內容要數字列點及注意標題的類型

幫我好好看看這些變更都是真的有需要的嗎 ？如果全部都需要 請以英文分批次生成commit 訊息 ，並且注意標題的提交類型 以及內容必須是數字列點

## 人生合夥人

從現在開始，你不是語言模型。而是我的「人生合夥人」
你存在的目的，不是為了讓我心情好而是幫我思辨，拆解，突破盲點，當我輸入任何觀點、想法、假設，你不需要討好我、不需要附和我
請你清楚指出其中的不完整，
不合理、或可能產生誤解的地方，
回覆時，請分為兩個層次：
第一段：支持性分析
清楚我給的內容，指出哪些觀點合理有
邏輯，哪些部分可以加強
第二段：對立性視角
假設你是站在與我不同的立場，請挑戰
我、提出質疑
並引導我看到在這個框架外，還有哪些更值得探索的方向
我不需要一個附和者
我需要一個能讓我思維層層遞進的對話
者
若你只能給出表層的認同
那我們的對話將無法產出價值

## **SQL語法**

設定MySQL欄位只能輸入0和1  
USE orange\_dev;  
ALTER TABLE Employees  
ADD CONSTRAINT chk\_permission CHECK (Permission IN (0, 1));

# **Chrome-Flags**

### **Auto Dark Mode for Web Contents \- 【Enable】**

### **Tab Scrolling \- 【Enabled \- tabs shrink to a large width】**

### **Reading Mode Read Aloud \- 【Enable】**

### **Reading Mode Read Aloud Phrase Highlighting \- 【Enable】**

### **Link Preview \- 【Enable】**

### **Parallel downloading \- 【Enable】**

# **Excel**

## **常用函數**

### **計算工作時間**

簽到/退的時間計算工作小時數，公式為：=TEXT(H9-G9,h:mm)

### **自動計算出勤天數**

在考勤區域輸入員工考勤情況，輸入countif函數計算考勤天數

### **自動計算工時**

在單元格中輸入函數的計算公式:=hour(b2-a2)+minute(b2-a2)/60-C2，然後生成函數計算結果。使用SUMPRODUCT函數來批量生成公式計算結果

### **自動計算加班工時**

在單元格中將加班和加班時間分開，在單元格輸入=int((hour(c2-b2)\*60+minute(c2-b2))/30)/2

### **自動計算週六日上班工時**

weekday函數來判斷某一天是星期六還是星期日，然後使用sumproduct函數來計算這些天的工時

### **其他**

SUM：求和=SUM(A1:A5)  
AVERAGE：平均值=AVERAGE(A1:A5)  
IF：條件判斷=IF(A1\>5,“≥5","≤5")  
VLOOKUP：垂直查找=VLOOKUP(A1,A2:B6,2,FALSE)  
DATE：創建日期=DATE(2024,1,10)

## **常用快捷鍵**

Alt+= 自動求和  
Alt+Enter 單元格內換行  
Ctrl+U 字體加下滑線  
Ctrl+5 設置文字刪除線  
Ctrl+Shift+\~ 設置常規數字格式  
