# System Prompts 系統提示詞集合

此資料夾存放各式系統提示詞（System Prompts），用於定義 AI 的角色、專業領域與核心邏輯。

## 📋 命名規範

檔案命名統一遵循：`{角色名稱}_{變體類型}.md`

- **角色名稱**：描述 AI 的核心職能（例如：`doc-processor`、`exam-consultant`）。
- **變體類型**：區分功能版本（例如：`profiles` 表示包含多個子角色、`base` 表示基礎版、`holographic` 表示全息深度版）。

---

## 📚 提示詞分類導覽

### 1. 知識消化與文件處理 (Document Digestion)
用於將大量原始資料轉化為結構化知識。

| 檔案 | 包含角色 (Profiles) | 核心用途 | 適用情境 |
| :--- | :--- | :--- | :--- |
| **[data-organization-expert_profiles.md](file:///c:/Users/g1014308/Documents/GitHub/Youchen/Method-List/resources/system-prompts/data-organization-expert_profiles.md)** | A, B, C, D | 讀取教材、摘要、深度原理重建、大文件拆解。 | 從零開始學習新文件，或需要將 100 頁以上的資料分段深潛。 |

> **Profile 說明：**
> *   **Profile A (Storyline)**: 串連前後文故事線。
> *   **Profile B (Concept)**: 原子級深度拆解，強制不簡化。
> *   **Profile C (Insight)**: 模擬同學/導師給予第三人稱回饋。
> *   **Profile D (Progressive)**: **分段閱讀器**，解決 Token 爆掉問題，分段強拆極厚文件。

### 2. 互動式學科教練 (Interactive Subject Coaching)
用於針對特定問題進行深度解答、解題或研究引導。

| 檔案 | 名稱 | 核心功能 | 適用情境 |
| :--- | :--- | :--- | :--- |
| **[exam-consultant_holographic.md](file:///c:/Users/g1014308/Documents/GitHub/Youchen/Method-List/resources/system-prompts/exam-consultant_holographic.md)** | 全息教材考題教練 | **答題器**：找證據、分析選項、理科運算與協議圖繪製。 | 準備考古題、練習作業題，需要 AI 展現 LaTeX 計算細節與證據溯源。 |
| **[research-advisor_base.md](file:///c:/Users/g1014308/Documents/GitHub/Youchen/Method-List/resources/system-prompts/research-advisor_base.md)** | 研究顧問助理 | **提案引導**：蘇格拉底式提問、研究動機與 SOTA 查核。 | 撰寫期末報告提案、碩博士論文研究開發階段。 |

### 3. 通用助理與開發工具 (Utilities)

| 檔案 | 說明 | 適用情境 |
| :--- | :--- | :--- |
| **[chat-assistants_collection.md](file:///c:/Users/g1014308/Documents/GitHub/Youchen/Method-List/resources/system-prompts/chat-assistants_collection.md)** | 包含喵大人、狐小健、林老師等角色，以及 Git Commit 自動生成器。 | 日常對話趣味性、Git 提交流程自動化。 |

### 4. 元提示詞指南 (Meta-Prompting)

| 檔案 | 說明 | 適用情境 |
| :--- | :--- | :--- |
| **[prompt-design-best-practices.md](file:///c:/Users/g1014308/Documents/GitHub/Youchen/Method-List/resources/system-prompts/prompt-design-best-practices.md)** | 提示詞設計的最佳實踐與規範。 | 當你需要自己設計或修改系統提示詞時的參考手冊。 |

---

## ⚡ 核心守則 (Global Guardrails)
所有專業 Profiles 皆受以下「天條」約束：
1. **No Hallucination**: 禁止捏造數據與引用。
2. **Pedagogical Logic**: 非僅給答案，而是透過深度解析引導學習。
3. **Depth Mandate**: 寧可詳細論述也不可點到為止，嚴禁暗示性的跳過（如「以此類推」）。
4. **Traditional Chinese**: 全程繁體中文輸出。

---
**最後更新：2026-04-11** (整合 Crypto 邏輯、區分 D 讀與教練答、統一命名規範)
