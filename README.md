# Method List - 技術方法與解決方案知識庫

[![GitHub](https://img.shields.io/badge/GitHub-Method--List-blue)](https://github.com/Youchenjiang/Method-List)
[![License](https://img.sh3. **學習理論概念**：
   - AI 概念：`Learning-Notes/ai/` - 人工智慧理論與概念
   - 量子科技：`Learning-Notes/Quantum/` - 量子計算與量子通訊lds.io/badge/License-MIT-green.svg)](LICENSE)

> 一個集合技術教學、工具資源與問題解決方案的綜合知識庫

## 📋 目錄

- [Method List - 技術方法與解決方案知識庫](#method-list---技術方法與解決方案知識庫)
  - [📋 目錄](#-目錄)
  - [🎯 專案介紹](#-專案介紹)
    - [主要特色](#主要特色)
  - [📁 資料夾結構](#-資料夾結構)
  - [📖 內容概覽](#-內容概覽)
    - [🛠️ Methods - 技術方法](#️-methods---技術方法)
      - [🤖 AI 相關技術 (Methods/ai/)](#-ai-相關技術-methodsai)
      - [💻 開發技術 (Methods/development/)](#-開發技術-methodsdevelopment)
      - [🔧 工具使用方法 (Methods/tools/)](#-工具使用方法-methodstools)
    - [📝 Learning-Notes - 學習筆記](#-learning-notes---學習筆記)
      - [🤖 AI 相關概念 (Learning-Notes/ai/)](#-ai-相關概念-learning-notesai)
      - [⚛️ 量子科技 (Learning-Notes/Quantum/)](#️-量子科技-learning-notesquantum)
    - [📚 Resources - 工具資源](#-resources---工具資源)
      - [💾 軟體工具 (Resources/software/)](#-軟體工具-resourcessoftware)
      - [📺 媒體資源 (Resources/media/)](#-媒體資源-resourcesmedia)
      - [🌐 線上服務 (Resources/online/)](#-線上服務-resourcesonline)
    - [🔧 Solutions - 解決方案](#-solutions---解決方案)
      - [🐛 開發問題 (Solutions/development/)](#-開發問題-solutionsdevelopment)
      - [💻 系統問題 (Solutions/system/)](#-系統問題-solutionssystem)
      - [🌐 網路問題 (Solutions/network/)](#-網路問題-solutionsnetwork)
  - [🚀 使用指南](#-使用指南)
    - [快速導航](#快速導航)
    - [搜尋技巧](#搜尋技巧)
    - [閱讀建議](#閱讀建議)
  - [🤝 貢獻指南](#-貢獻指南)
    - [貢獻方式](#貢獻方式)
    - [內容規範](#內容規範)
    - [文件命名規則](#文件命名規則)
    - [計劃更新](#計劃更新)
  - [📞 聯絡資訊](#-聯絡資訊)
  - [📄 授權條款](#-授權條款)

## 🎯 專案介紹

Method List 是一個專門收集和整理技術方法、工具資源和問題解決方案的知識庫。旨在為開發者、技術愛好者和學習者提供一個便於查找和學習的資源平台。

### 主要特色

- ✅ **系統化分類**：按照方法、資源、解決方案三大類別組織內容
- ✅ **詳細教學**：提供步驟詳細的操作指南和截圖說明
- ✅ **實用工具**：收錄各類實用軟體工具和線上服務
- ✅ **問題解決**：整理常見技術問題的解決方案
- ✅ **持續更新**：定期更新內容，保持資訊的時效性

## 📁 資料夾結構

```tree
Method-List/
├── README.md                                    # 專案說明文件
├── Methods/                                     # 技術方法與教學
│   ├── ai/                                     # AI 相關技術
│   │   └── azure-openai-analyze-pdf.md        # Azure OpenAI PDF 分析教學
│   ├── development/                            # 開發技術
│   │   └── vs2022-import-excel.md              # VS2022 匯入 Excel 資料方法
│   └── tools/                                  # 工具使用方法
├── Learning-Notes/                              # 學習筆記與概念整理
│   ├── ai/                                     # AI 相關概念
│   │   ├── ai-machine-learning-concepts.md    # AI 領域知識全景圖
│   │   ├── ai-schools-symbolic-connectionist.md # AI 思想體系學派分析
│   │   └── ai-classification-frameworks-comparison.md # AI 分類框架對比分析
│   └── Quantum/                                # 量子科技相關
│       └── quantum-research.md                # 量子研究筆記
├── Resources/                                   # 工具資源整理
│   ├── software/                               # 軟體工具
│   │   ├── software-tools-computer.md         # 電腦軟體工具大全
│   │   └── software-tools-phone.md            # 手機軟體工具
│   ├── media/                                  # 媒體資源
│   │   ├── media-channel-classification.md    # 影音頻道分類
│   │   ├── music-collection.md                # 音樂收藏
│   │   └── video-collection.md                # 影片收藏
│   ├── tools/                                  # 工具使用方法
│   │   └── computer-commands-reference.md     # 電腦指令參考大全
│   └── online/                                 # 線上服務
│       └── software-tools-web.md              # 網頁工具服務
└── Solutions/                                   # 問題解決方案
    ├── development/                            # 開發問題
    │   ├── github-clone-failed.md             # GitHub Clone 失敗解決方案
    │   └── python-environment-error.md        # Python 環境錯誤解決方案
    ├── system/                                 # 系統問題
    └── network/                                # 網路問題
```

## 📖 內容概覽

### 🛠️ Methods - 技術方法

#### 🤖 AI 相關技術 ([Methods/ai/](Methods/ai/))

| 文件名稱 | 描述 | 難度 | 標籤 |
|---------|------|------|------|
| [Azure OpenAI PDF 分析](Methods/ai/azure-openai-analyze-pdf.md) | 使用 Azure OpenAI 分析 PDF 文件的完整教學 | 中級 | `Azure` `OpenAI` `Python` `RAG` |

#### 💻 開發技術 ([Methods/development/](Methods/development/))

| 文件名稱 | 描述 | 難度 | 標籤 |
|---------|------|------|------|
| [VS2022 匯入 Excel](Methods/development/vs2022-import-excel.md) | Visual Studio 2022 匯入 Excel 資料到 SQL Server 的方法 | 初級 | `VS2022` `Excel` `SQL Server` |

#### 🔧 工具使用方法 ([Methods/tools/](Methods/tools/))

（待新增內容）

### 📝 Learning-Notes - 學習筆記

#### 🤖 AI 相關概念 ([Learning-Notes/ai/](Learning-Notes/ai/))

| 文件名稱 | 描述 | 類型 | 標籤 |
|---------|------|------|------|
| [AI 領域知識全景圖](Learning-Notes/ai/ai-machine-learning-concepts.md) | 人工智慧、機器學習與各種學習方式的概念解析 | 概念筆記 | `AI` `機器學習` `概念解析` `學習筆記` |
| [AI 思想體系三大學派](Learning-Notes/ai/ai-schools-symbolic-connectionist.md) | 符號主義、連結主義、行為主義三大AI學派的思想分析 | 思想史筆記 | `符號主義AI` `連結主義AI` `行為主義AI` `AI學派` `思想體系` |
| [AI 分類框架對比分析](Learning-Notes/ai/ai-classification-frameworks-comparison.md) | 功能導向與思想體系分類的對比，「番茄悖論」方法論探討 | 方法論筆記 | `分類框架` `方法論` `番茄悖論` `多維度分析` |

#### ⚛️ 量子科技 ([Learning-Notes/Quantum/](Learning-Notes/Quantum/))

| 文件名稱 | 描述 | 類型 | 標籤 |
|---------|------|------|------|
| [量子研究筆記](Learning-Notes/Quantum/quantum-research.md) | 量子計算、量子通訊等前沿科技研究筆記 | 研究筆記 | `量子計算` `量子通訊` `前沿科技` `研究筆記` |

### 📚 Resources - 工具資源

#### 💾 軟體工具 ([Resources/software/](Resources/software/))

| 文件名稱 | 描述 | 內容數量 |
|---------|------|---------|
| [電腦軟體工具大全](Resources/software/software-tools-computer.md) | 電腦端各類軟體工具分類整理 | 200+ 工具 |
| [手機軟體工具](Resources/software/software-tools-phone.md) | 手機端實用 APP 推薦 | - |

#### 📺 媒體資源 ([Resources/media/](Resources/media/))

| 文件名稱 | 描述 | 內容數量 |
|---------|------|---------|
| [影音頻道分類](Resources/media/media-channel-classification.md) | YouTube、Bilibili、Facebook 優質頻道整理 | 300+ 頻道 |
| [音樂收藏](Resources/media/music-collection.md) | 音樂收藏整理 | - |
| [影片收藏](Resources/media/video-collection.md) | 影片收藏整理 | - |

#### 🔧 工具使用方法 ([Resources/tools/](Resources/tools/))

| 文件名稱 | 描述 | 內容數量 |
|---------|------|---------|
| [電腦指令參考大全](Resources/tools/computer-commands-reference.md) | CMD、PowerShell、Git 等常用指令整理 | 50+ 指令 |

#### 🌐 線上服務 ([Resources/online/](Resources/online/))

| 文件名稱 | 描述 | 內容數量 |
|---------|------|---------|
| [網頁工具服務](Resources/online/software-tools-web.md) | 線上工具和網頁服務整理 | - |

### 🔧 Solutions - 解決方案

#### 🐛 開發問題 ([Solutions/development/](Solutions/development/))

| 文件名稱 | 描述 | 問題類型 |
|---------|------|---------|
| [GitHub Clone 失敗](Solutions/development/github-clone-failed.md) | 解決 GitHub 專案複製失敗的問題 | 版本控制 |
| [Python 環境錯誤](Solutions/development/python-environment-error.md) | Python 套件安裝和環境問題解決方案 | 開發環境 |

#### 💻 系統問題 ([Solutions/system/](Solutions/system/))

（待新增內容）

#### 🌐 網路問題 ([Solutions/network/](Solutions/network/))

（待新增內容）

## 🚀 使用指南

### 快速導航

1. **尋找教學方法**：
   - AI 技術：`Methods/ai/` - 人工智慧相關教學
   - 開發技術：`Methods/development/` - 程式開發方法
   - 工具使用：`Methods/tools/` - 各種工具的使用教學

2. **學習理論概念**：
   - AI 概念：`Learning-Notes/ai/` - 人工智慧理論與概念
   - 量子科技：`Learning-Notes/Quantum/` - 量子計算與量子通訊

3. **查找工具資源**：
   - 軟體工具：`Resources/software/` - 電腦和手機軟體推薦
   - 媒體資源：`Resources/media/` - 優質頻道和創作者
   - 工具使用：`Resources/tools/` - 常用指令和工具操作方法
   - 線上服務：`Resources/online/` - 網頁工具和雲端服務

4. **解決技術問題**：
   - 開發問題：`Solutions/development/` - 程式開發相關問題
   - 系統問題：`Solutions/system/` - 作業系統和硬體問題
   - 網路問題：`Solutions/network/` - 網路連線和安全問題

### 搜尋技巧

- 使用 GitHub 的搜尋功能在整個專案中搜尋關鍵字
- 利用文件中的標籤和分類快速定位內容
- 查看文件開頭的目錄結構快速跳轉

### 閱讀建議

- 每個教學都包含詳細步驟和截圖說明
- 注意查看參考資料和相關連結
- 建議按照步驟順序操作，避免跳過重要設定

## 🤝 貢獻指南

歡迎大家為這個知識庫貢獻內容！

### 貢獻方式

1. **Fork** 本專案
2. 建立新的分支 (`git checkout -b feature/new-method`)
3. 提交你的更改 (`git commit -am 'Add new method'`)
4. 推送到分支 (`git push origin feature/new-method`)
5. 建立 **Pull Request**

### 內容規範

- 使用繁體中文撰寫
- 提供詳細的步驟說明
- 包含必要的截圖或圖片
- 標註參考資料來源
- 遵循現有的文件格式

### 文件命名規則

- 使用小寫英文字母
- 單字間使用連字符 (`-`) 連接
- 使用描述性的文件名
- 例如：`azure-openai-tutorial.md`

### 計劃更新

- [ ] 增加更多 AI 相關教學與實作案例
- [ ] 擴充移動端工具資源和使用教學
- [ ] 新增更多開發環境問題解決方案
- [ ] 完善量子科技相關學習筆記
- [ ] 增加更多媒體資源收藏整理
- [ ] 建立工具評測和比較文章

## 📞 聯絡資訊

如果你有任何問題、建議或想要貢獻內容，歡迎聯絡：

- 💬 GitHub Issues: [提交問題或建議](https://github.com/Youchenjiang/Method-List/issues)

## 📄 授權條款

本專案採用 [MIT 授權條款](LICENSE)，歡迎自由使用和分享。

---

⭐ 如果這個專案對你有幫助，歡迎給我們一個 Star！
