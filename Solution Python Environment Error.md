
【問題】Python3.14無法安裝numpy

![image](https://github.com/user-attachments/assets/5ba0a2ac-1383-46ee-b4c5-ff12db7f3f8e)

【解法】改用Python3.14以下版本安裝numpy

---

【問題】Python3.12安裝face-detector出現版本錯誤

![image](https://github.com/user-attachments/assets/2a9d1d4e-c8ec-49bd-9008-a1cd99110a15)

【解法】改用Python3.4~3.9版本

`py -0`: 列出當前安裝的所有Python版本(*)表示預設執行環境

`py -3.14 install numpy`: 在3.14版本環境安裝numpy

可以直接安裝[Python3.9.13](https://www.python.org/downloads/release/python-3913/)，再進行套件安裝
 
face-detector依賴的absl-py判斷python版本的問題(v3.10以上判斷為小於v3.4)，[所以跳出版本過低問題](https://stackoverflow.com/questions/75250036/runtimeerror-python-version-2-7-or-3-4-is-required-even-if-i-already-have-3-10)，目前嘗試的其他繞過限制方法失敗

▼ 先選擇3.9的環境，再安裝cvzone,mediapipe,face-detector
 ![image](https://github.com/user-attachments/assets/0cf15d68-ecf0-4361-b2a6-1ec90a9c5dd9)

▼ face-detector安裝成功
![image](https://github.com/user-attachments/assets/301e4d7a-d616-48d6-a714-2a0027321746)

---

【問題】
【解法】

![image](https://github.com/user-attachments/assets/21987403-1ef6-4f20-8f04-649d331238b7)
