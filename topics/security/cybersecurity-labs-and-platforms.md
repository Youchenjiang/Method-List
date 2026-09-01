# 🌐 網路安全學習平台與實務靶場大全 (Cybersecurity Labs & Platforms Hub)

> 📌 **來源與整合說明**：本清單完整匯整自 [飛飛的資安學習筆記](https://feifei.tw/ctf-beginners-guide-resources/) 以及主流社群/抖音精選之資安學習平台、Web 漏洞靶場、內網滲透環境與 CTF 練習資源，依據**實務導向、學習曲線與特定技術分類**進行高濃度整理。

---

## 📋 目錄

- [🎓 1. 新手入門與互動式學習平台](#-1-新手入門與互動式學習平台)
- [⚔️ 2. 實戰滲透與 CTF 競賽平台](#️-2-實戰滲透與-ctf-競賽平台)
- [🛡️ 3. 經典 Web 漏洞專項靶場](#️-3-經典-web-漏洞專項靶場)
- [🐳 4. Docker 模組化與本地離線靶場](#-4-docker-模組化與本地離線靶場)
- [🏢 5. 內網滲透與企業域控靶場](#-5-內網滲透與企業域控靶場)
- [📚 6. 社群資源與參考知識庫](#-6-社群資源與參考知識庫)

---

## 🎓 1. 新手入門與互動式學習平台

| 平台名稱 | 核心亮點與特色 | 適合對象與技術焦點 | 官方連結 |
| :--- | :--- | :--- | :--- |
| **picoCTF** | CMU 主辦，針對新手設計，含常態 Gym 練習區，題目循序漸進。 | **新手首選**，CTF 全領域入門 | [picoCTF 官網](https://picoctf.org/) |
| **OverTheWire** | 經典 Linux CLI 闖關靶場 (Bandit)，從最基礎命令行操作開始教學。 | **CLI 新手**，Linux 系統操作 | [OverTheWire 官網](https://overthewire.org/) |
| **Hacksplaining** | 分步驟互動式引導教學，每個知識點皆有詳細操作指引。 | **零基礎入門**，Web 安全原理 | [Hacksplaining 官網](https://www.hacksplaining.com/) |
| **TryHackMe (THM)** | 關卡式學習與路徑化課程，提供雲端虛擬機，學習曲線平緩。 | **新手首選**，滲透測試基礎 | [TryHackMe 官網](https://tryhackme.com/) |
| **Hackertest** | 20 個漸進式關卡之趣味闖關網站，僅需基本 HTML 知識即可挑戰。 | **前端入門**，基礎 HTML/Web 分析 | [Hackertest 官網](http://www.hackertest.net/) |
| **WebGoat** | OWASP 官方出品，理論與實操結合，含 30+ 課程與視頻指導。 | **Web 安全基礎**，OWASP 漏洞理論 | [WebGoat 官網](https://owasp.org/www-project-webgoat/) |
| **Hacker101 CTF** | HackerOne 官方提供，偏向 Web 漏洞實操與 Bug Bounty 入門。 | **Web 滲透**，Web 漏洞與獎勵計劃 | [Hacker101 官網](https://ctf.hacker101.com/) |

---

## ⚔️ 2. 實戰滲透與 CTF 競賽平台

| 平台名稱 | 核心亮點與特色 | 適合對象與技術焦點 | 官方連結 |
| :--- | :--- | :--- | :--- |
| **Hack The Box (HTB)** | 國際頂尖滲透平台，模擬真實企業環境，含網站滲透、系統提權全流程。 | **中高階玩家**，真實主機滲透 | [Hack The Box 官網](https://www.hackthebox.com/) |
| **Root-Me** | 免費線上資安練習平台，包含 171 個虛擬環境、534+ 個挑戰題目。 | **中初階學習者**，全方位資安技能 | [Root-Me 官網](https://www.root-me.org/) |
| **RingZeroTeam** | 專業 CTF 訓練平台，提供 19 個類別、300+ 挑戰題目。 | **進階 CTF 選手**，系統化解題 | [RingZeroTeam 官網](https://ringzer0ctf.com/) |
| **攻防世界 (XCTF)** | 國內頂級 CTF 與靶場平台，免費開放，題目涵蓋多領域。 | **CTF 競賽選手**，解題實戰 | [攻防世界 官網](https://adworld.xctf.org.cn/) |
| **Bugku 靶場** | 老牌資安與 CTF 練習平台，題量超全、分類豐富。 | **CTF 新手至中階**，Web/Crypto/Misc | [Bugku 官網](https://ctf.bugku.com/) |
| **墨者學院** | 在線免搭建，邊學邊練，提供豐富實例與真實漏洞環境。 | **實戰練習**，線上漏洞演練 | [墨者學院 官網](https://www.mozhe.cn/) |

---

## 🛡️ 3. 經典 Web 漏洞專項靶場

| 靶場名稱 | 核心亮點與特色 | 專項練習領域 | 官方/取得連結 |
| :--- | :--- | :--- | :--- |
| **DVWA** (Damn Vulnerable Web App) | Web 安全入門標桿，OWASP Top 10 全覆蓋，提供 4 級難度可調。 | **Web 入門必練**，SQLi, XSS, CSRF | [DVWA 官網](https://dvwa.co.uk/) |
| **Pikachu 靶場** | 中文介面友好、漏洞分類清晰、零基礎無壓力。 | **中文新手**，Web 基礎漏洞全套 | [Pikachu GitHub](https://github.com/zhu峰/pikachu) |
| **SQLi-Labs** | SQL 注入專項靶場，涵蓋報錯注入、盲注、堆疊注入等全類型。 | **SQL 注入專戰**，各類 SQLi 繞過 | [SQLi-Labs GitHub](https://github.com/Audi-1/sqli-labs) |
| **Upload-Labs** | 20+ 檔案上傳繞過場景，涵蓋前端/後端/解析漏洞。 | **檔案上傳專戰**，WebShell 上傳 | [Upload-Labs GitHub](https://github.com/cjw2017/upload-labs) |

---

## 🐳 4. Docker 模组化與本地離線靶場

| 靶場名稱 | 核心亮點與特色 | 部署與使用方式 | 官方連結 |
| :--- | :--- | :--- | :--- |
| **VulnHub** | 免費虛擬機鏡像下載，本地離線無網路限制，適合內網練習。 | 下載 `.iso` / `.ova` 於 VMware 離線運行 | [VulnHub 官網](https://www.vulnhub.com/) |
| **Vulhub** | 基於 Docker 的漏洞環境集合，一鍵啟動復現最新 CVE 漏洞。 | `docker-compose up -d` 一鍵部署復現 | [Vulhub 官網](https://vulhub.org/) |
| **Vulfocus** | Docker 一鍵起漏洞復現平台，鏡像下載快且存取穩定。 | 網頁端或 Docker 一鍵開啟漏洞 | [Vulfocus 官網](https://vulfocus.cn/) |

---

## 🏢 5. 內網滲透與企業域控靶場

| 靶場名稱 | 核心亮點與特色 | 專項技術焦點 |
| :--- | :--- | :--- |
| **VulnStack (紅日靶場)** | 內網滲透標桿，還原企業真實多層內網、域控票據與橫向移動。 | **內網與 AD 域控**，域滲透、Cobalt Strike |
| **TRY HARDER (OSCP 實戰)** | 100+ OSCP 同款場景，像素畫風 + 無限重試，支援導出操作日誌。 | **OSCP 認證備考**，Metasploit 實戰、Python 提權 |

---

## 📚 6. 社群資源與參考知識庫

| 資源名稱 | 簡介與說明 | 連結 |
| :--- | :--- | :--- |
| **TW-Security-and-CTF-Resource** | 台灣資安社群 Ice1187 整理之熱門工具與學習資源清單 | [GitHub - TW-Security](https://github.com/Ice1187/TW-Security-and-CTF-Resource) |
| **CTF Wiki** | 全面且系統化的 CTF 英文/中文技術知識庫 | [CTF Wiki 官網](https://ctf-wiki.org/) |
| **CTFTime** | 全球 CTF 賽事日程、戰隊積分排名與歷史 Writeups 庫 | [CTFTime 官網](https://ctftime.org/) |
| **GitHub - ctfs** | 全球 CTF 賽事解題報告 (Writeup) 匯整倉庫 | [GitHub - ctfs](https://github.com/ctfs) |
| **AIS3 官方網站** | 台灣教育部資安人才培育計畫與課程賽事資訊 | [AIS3 官網](https://ais3.org/) |
