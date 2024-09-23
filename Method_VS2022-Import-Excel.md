# Visual Studio 2022 新版 SQL Server 匯入 EXCEL 資料方法  
說明：下文分別使用1,2,3表示不同軟體間操作  
-
1.表示Visual Studio 2022  
2.表示SQL Server Management Studio 20  
3.表示在本機上操作

首先開啟VS2022
-
1-1.在「Visual Studio 2022」開啟(或建立)專案後，在「方案總管」的網站處右鍵，選擇加入/加入新項目  
<img width="400" height="200" src="/Image/1-1.png"/>   
1-2.選擇加入「SQL Server資料庫」  
<img width="250" height="200" src="/Image/1-2.png"/>   
1-3.點擊新建的「Database1.mdf」，使得伺服器總管中的Database1.mdf為綠色圖標  
<img width="200" height="200" src="/Image/1-3.png"/>   
1-4.開啟工具/選項，在最下方的資料庫工具中找到資料連接，並複製SQL Server執行個體名稱「(LocalDB)\MSSQLLocalDB」  
<img width="300" height="200" src="/Image/1-4.png"/>   

接下來就可以在SSMS中作操作  
-
2-1.連線至伺服器畫面貼上1.4步驟的伺服器名稱，並選擇Windows驗證  
<img width="300" height="200" src="/Image/2-1.png"/>   
2-2.點擊連線後，點擊物件總管/工作/匯入資料  
<img width="300" height="200" src="/Image/2-2.png"/>   
2-3.開啟匯入匯出精靈後，選擇「Next>」  
<img width="300" height="200" src="/Image/2-3.png"/>   
2-4.資料來源處選擇「Microsoft Excel」，點擊「Next>」  
<img width="300" height="200" src="/Image/2-4.png"/>  
2-5.會出現「'Microsoft.ACE.OLEDB.12.0' 提供者並未登錄於本機電腦上」錯誤，因此需下載擴充套件
<img width="450" height="200" src="/Image/2-5.png"/>  

開啟瀏覽器
-
3-1.在瀏覽器中搜尋[Microsoft Access Database Engine 2016 可轉散發套件](https://www.microsoft.com/zh-tw/download/details.aspx?id=54920)  
<img width="400" height="200" src="/Image/3-1.png"/>  
3-2.將它存在「下載」目錄底下  
<img width="550" height="200" src="/Image/3-2.png"/>  
3-3.點擊「accessdatabaseengine_X64.exe」，安裝在「C:\Program Files\Microsoft Office\」資料夾內  
<img width="300" height="200" src="/Image/3-3.png"/>  
3-4.在「下載」資料夾下，右鍵後點擊「在終端中開啟」(無圖)  
輸入「cmd」，點擊Enter，輸入「AccessDatabaseEngine.exe /quiet」，點擊Enter，即可關閉視窗  
<img width="300" height="200" src="/Image/3-4.png"/>  

安裝完擴充套件，回到SSMS
-
2-6.回到第2-1步驟，此時已經可以點擊「Next>」  
<img width="300" height="200" src="/Image/2-6.png"/>    
2-7.更改目的地為「Microsoft OLE DB Driver」  
<img width="300" height="200" src="/Image/2-7.png"/>   
2-8.點擊屬性，進入「資料連結內容」，將1-4步驟中的伺服器名稱貼上、選擇Windows驗證、選擇Database1.mdf資料庫，確定後即可進入下一步  
<img width="200" height="200" src="/Image/2-8.png"/>   
2-9.點擊「Next>」直到最後、點擊Finish  
<img width="280" height="200" src="/Image/2-9.png"/>   
2-10.在伺服器總管中可見匯入成功  
<img width="200" height="200" src="/Image/2-10.png"/>   

打開VS2022
-
1-5.在伺服器總管點擊重新整理，可見匯入成功🎉  
<img width="200" height="200" src="/Image/1-5.png"/> 

參考資料：
-
1.[How to fix the SQL error Microsoft.ACE.OLEDB.16.0' provider is not registered on the local machine.](https://www.youtube.com/watch?v=t7C151yxwcY)  
2.[Uncovering the Alternative to the Missing SQL Server Native Client - What You Need to Know!](https://www.youtube.com/watch?v=SA4La3eLUPY)  
