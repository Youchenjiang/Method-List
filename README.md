# Github-Clone-Failed
Describe how to solve "Github Clone Failed" Problem


![image](https://github.com/user-attachments/assets/c66ddad1-c669-4c70-b7a5-04f685be1750)

來到「準備存放儲存庫的資料夾」
![image](https://github.com/user-attachments/assets/1ec525b7-aadc-4b76-ae68-971e45f9f32c)

在路徑處輸入cmd
![image](https://github.com/user-attachments/assets/5e9f9a8b-af5e-4fc4-bd5d-15e655862fd4)

git config --global core.compression 0 
(試著關閉在複製專案時，複製壓縮的內容，但這會讓複製專案的過程變慢。)
![image](https://github.com/user-attachments/assets/40a950ab-14db-41bc-990a-fa26a8118067)

git config --global http.postBuffer 524288000
(在複製專案時，設定並加大較大的buffer size。)
![image](https://github.com/user-attachments/assets/2ffbe095-fa68-4a37-93a3-71adeb06bd0f)

複製「專案Clone網址」
![image](https://github.com/user-attachments/assets/8e353b7e-a717-44a5-ace1-407d0152c1ce)

git clone 「專案Clone網址」
![image](https://github.com/user-attachments/assets/7efcf94f-d50e-4305-a877-21ea558d2cb5)

成功複製儲存庫
![image](https://github.com/user-attachments/assets/7277efb3-aa84-4c6e-a643-f92fa7d41466)

回到Github Desktop，選擇Add Local Repository
![image](https://github.com/user-attachments/assets/3cc9451f-de0c-40fe-8731-1a09e24e6640)

選擇剛才的「準備存放儲存庫的資料夾」
![image](https://github.com/user-attachments/assets/42a6a132-69ed-4d09-b838-097e201c5628)

參考：
[如何避免Git clone指令在複製大專案時候出錯？](https://peterli.website/%E5%A6%82%E4%BD%95%E9%81%BF%E5%85%8Dgit-clone%E6%8C%87%E4%BB%A4%E5%9C%A8%E8%A4%87%E8%A3%BD%E5%A4%A7%E5%B0%88%E6%A1%88%E6%99%82%E5%80%99%E5%87%BA%E9%8C%AF%EF%BC%9F/)
