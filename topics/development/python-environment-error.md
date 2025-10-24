Windows操作Python
---

【問題】無法使用pip

![image](https://github.com/user-attachments/assets/383974b8-e78c-4fac-ae03-615ac308d670)

【解法1】繼續使用Python環境，加上 -m 指令

`python -m pip`

![image](https://github.com/user-attachments/assets/ed8e3cc0-de84-48f0-86ac-d2c740202a11)

【解法2】退出Python環境，直接使用pip

輸入 quit() 或是點擊鍵盤 Ctrl-Z 退出python運行環境

`pip` 直接使用pip

![image](https://github.com/user-attachments/assets/895fc0ba-12d2-416f-9821-cb90f2a6ba5d)


---

【問題】Python3.14無法安裝numpy

![image](https://github.com/user-attachments/assets/5ba0a2ac-1383-46ee-b4c5-ff12db7f3f8e)

【解法】改用Python3.14以下版本安裝numpy

---

【問題】Python3.12安裝face-detector出現版本錯誤

![image](https://github.com/user-attachments/assets/2a9d1d4e-c8ec-49bd-9008-a1cd99110a15)

【解法】改用Python3.4~3.9版本

`py -0`: 列出當前安裝的所有Python版本(*)表示預設執行環境

`py -3.14 install numpy`: 在3.14版本環境安裝numpy

`pip install --verbose numpy`: --verbose參數可提供安裝出錯詳細原因

可以直接安裝[Python3.9.13](https://www.python.org/downloads/release/python-3913/)，再進行套件安裝
 
face-detector依賴的absl-py套件無法有效比較python3.9以上版本(v3.10以上判斷為小於v3.4)，所以跳出版本過低問題(參考以下)，嘗試的其他繞過限制方法均失敗

[RuntimeError: Python version 2.7 or 3.4+ is required even if I already have 3.10.6 version](https://stackoverflow.com/questions/75250036/runtimeerror-python-version-2-7-or-3-4-is-required-even-if-i-already-have-3-10) 

[How solve "python setup.py egg_info did not run successfully" in Anaconda, installing rasa](https://stackoverflow.com/questions/76887424/how-solve-python-setup-py-egg-info-did-not-run-successfully-in-anaconda-insta)

[pip install安装的时候在Preparing metadata (setup.py) ...卡住](https://blog.csdn.net/sinat_29957455/article/details/130285223)

[多版本 Python 使用 pip 安装 package](https://blog.csdn.net/DunkyZ/article/details/128091318)

[Python: Python 多版本管理](https://magicjackting.pixnet.net/blog/post/225113189)

[python学习笔记（1）----python安装](https://www.cnblogs.com/wanghaihong200/p/7587326.html)

▼ 先選擇3.9的環境，再安裝cvzone,mediapipe,face-detector
 ![image](https://github.com/user-attachments/assets/0cf15d68-ecf0-4361-b2a6-1ec90a9c5dd9)

▼ face-detector安裝成功
![image](https://github.com/user-attachments/assets/301e4d7a-d616-48d6-a714-2a0027321746)

---

【問題】

「ImportError: DLL load failed while importing _framework_bindings: 找不到指定的模塊。」


![image](https://github.com/user-attachments/assets/21987403-1ef6-4f20-8f04-649d331238b7)

【解法】

將Anaconda更新到最新版、執行`conda update --all`

---
【問題】
「UnicodeDecodeError: 'cp950' codec can't decode byte 0xf0 in position 2391: illegal multibyte sequence」

![image](https://github.com/user-attachments/assets/bc294cfb-be48-4384-81f0-ca811c250738)

【解法】
切換Vscode左下角UTF-8編碼為UTF-8 with BOM，重新儲存，即可正常繼續安裝環境

![image](https://github.com/user-attachments/assets/422e24c0-7d77-497c-a565-e6f73eb4f8ea)