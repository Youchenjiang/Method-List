# Method List - 技術方法與解決方案知識庫

[Read in English](README.md)

[![GitHub](https://img.shields.io/badge/GitHub-Method--List-blue)](https://github.com/Youchenjiang/Method-List)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> 一個集合技術教學、工具資源與問題解決方案的綜合知識庫

## 目錄

- [Method List - 技術方法與解決方案知識庫](#method-list---技術方法與解決方案知識庫)
  - [目錄](#目錄)
  - [專案介紹](#專案介紹)
  - [資料夾結構](#資料夾結構)
  - [內容概覽](#內容概覽)
    - [📚 Topics - 主題文章](#-topics---主題文章)
    - [🗂️ Resources - 資源彙整](#️-resources---資源彙整)
  - [貢獻指南](#貢獻指南)
  - [聯絡資訊](#聯絡資訊)
  - [授權條款](#授權條款)

## 專案介紹

Method List 是一個專門收集和整理技術方法、工具資源和問題解決方案的知識庫。旨在為開發者、技術愛好者和學習者提供一個便於查找和學習的資源平台。

## 資料夾結構

```tree
Method-List/
├── README.md
├── resources/
│   ├── agent-rules/     # AI agent 行為規則（可貼進 CLAUDE.md / AGENTS.md）
│   ├── media/          # 媒體頻道與收藏
│   ├── online/         # 網頁工具與服務
│   ├── software/       # 軟體推薦
│   ├── system-prompts/ # AI 助理提示詞模板
│   ├── tools/          # 指令參考與快捷鍵
│   └── github/         # GitHub 儲存庫參考
└── topics/
    ├── ai/             # AI 與機器學習
    │   └── machine-learning/  # ML 作業報告、論文摘要
    ├── data-engineering/ # 資料工程概念
    ├── development/    # 開發除錯
    ├── mindset/        # 個人心態與反思
    ├── quantum/        # 量子計算研究
    ├── research-method/ # 研究方法課程學習筆記
    ├── security/       # 資訊安全
    └── technology/     # 硬體與軟體問答
```

## 內容概覽

本知識庫主要分為兩大部分：

### 📚 Topics - 主題文章

依領域組織的深入技術文章、教學與問題解決方案：

- **AI** ([topics/ai/](topics/ai/)) - 人工智慧、機器學習、Azure OpenAI
  - **機器學習** ([topics/ai/machine-learning/](topics/ai/machine-learning/)) - ML 作業報告、論文摘要、特徵選擇研究
- **資料工程** ([topics/data-engineering/](topics/data-engineering/)) - 資料處理與工程概念
- **開發** ([topics/development/](topics/development/)) - 程式除錯與開發工具
- **心態** ([topics/mindset/](topics/mindset/)) - 個人心態與反思
- **量子** ([topics/quantum/](topics/quantum/)) - 量子計算研究
- **研究方法** ([topics/research-method/](topics/research-method/)) - 研究方法課程學習筆記（中央大學）
- **安全** ([topics/security/](topics/security/)) - 資訊安全概念、靶場實戰與維運指令
  - **學習平台與靶場** ([topics/security/cybersecurity-labs-and-platforms.md](topics/security/cybersecurity-labs-and-platforms.md)) - TryHackMe, HTB, DVWA 等線上/本地靶場
  - **CTF 競賽指南** ([topics/security/ctf-beginner-guide.md](topics/security/ctf-beginner-guide.md)) - 6 大領域題型、8 大賽制模式與解題 SOP
  - **考試與名詞速查** ([topics/security/information-security-notes.md](topics/security/information-security-notes.md)) - 認證協定（OAuth/SAML/OIDC）、AAA 與高頻考點對比
  - **維運指令 Cheatsheet** ([topics/security/network-security-cheatsheet.md](topics/security/network-security-cheatsheet.md)) - Nmap 掃描、Wireshark/tcpdump 過濾與防火牆規則
  - **自動化安全分析** ([topics/security/automation-analysis-logic.md](topics/security/automation-analysis-logic.md)) - 程式碼安全測試 Phase 1 意圖分析與污點追蹤邏輯
- **技術** ([topics/technology/](topics/technology/)) - 硬體與軟體問答

### 🗂️ Resources - 資源彙整

精選的工具、軟體、媒體與參考資料集合：

- **Agent 行為規則** ([resources/agent-rules/](resources/agent-rules/)) - 可複用的 AI agent 行為規則。複製貼上到你的 CLAUDE.md / AGENTS.md 即可改善 agent 的問題解決能力。
- **媒體** ([resources/media/](resources/media/)) - YouTube 頻道、音樂與影片收藏
- **線上** ([resources/online/](resources/online/)) - 網頁工具與服務
- **軟體** ([resources/software/](resources/software/)) - 電腦與手機應用程式推薦
- **系統提示詞** ([resources/system-prompts/](resources/system-prompts/)) - AI 助理提示詞模板（例如 `data-organization-expert_profiles.md`，單檔整合故事串聯/深度拆解/第三人稱觀點三種 Profile 與 Turbo 模組） → [詳細內容](resources/system-prompts/)
- **工具** ([resources/tools/](resources/tools/)) - 指令參考、快捷鍵與**快速修復指令** → [詳細內容](resources/tools/)
- **GitHub 參考** ([resources/github/](resources/github/)) - 精選具價值的 GitHub 儲存庫清單

## 貢獻指南

歡迎為此知識庫貢獻內容！請參考現有的分類結構，將您的文件放在 `topics` 或 `resources` 資料夾中，並提交 Pull Request。

## 聯絡資訊

若有任何問題或建議，歡迎透過 [GitHub Issues](https://github.com/Youchenjiang/Method-List/issues) 提出。

## 授權條款

本專案採用 [MIT 授權條款](LICENSE)，歡迎自由使用和分享。

---

如果這個專案對你有幫助，歡迎給我們一個 Star！