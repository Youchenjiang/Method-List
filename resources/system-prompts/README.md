# System Prompts 系統提示詞集合

此資料夾存放各式系統提示詞（System Prompts），用於定義 AI 的角色、專業領域與核心邏輯。

## 📋 命名規範

檔案命名統一遵循：`{類別}_{角色名稱}_{變體模式}.md` (變體模式僅在有特殊機制時標註)

### 類別說明 (Categories)
- **`digest`**：知識消化與文件處理角色，用於讀取教材、深度拆解或長文拆分。
- **`coach`**：互動式學科教練或顧問角色，用於解題、研究引導或蘇格拉底式對話。
- **`util`**：通用型助理與日常開發工作輔助工具。
- **`meta`**：提示詞設計規範與相關元件定義。

---

## 快速選擇指南 (Selector Guide)

```text
┌──────────────────────────────────┐
│      你要 AI 幫你處理什麼任務？  │
└────────────────┬─────────────────┘
                 │
        ┌────────┴────────┐
        ▼                 ▼
  📖 [ 知識消化 ]    🎓 [ 互動教練 ]
     (Digestion)        (Coaching)
        │                 │
        │                 ├───────► 📝 寫題、解題、對答案？
        │                 │         ➜ coach_exam-consultant_holographic.md
        │                 │
        │                 └───────► 🔬 構思研究、寫論文提案？
        │                           ➜ coach_research-advisor.md
        │
        ├──────────► 📚 資料超級厚 (100頁+)，怕漏看？
        │           ➜ digest_document-shredder_progressive.md
        │
        ├──────────► 💎 內容好難懂，想原子級深度拆解？
        │           ➜ digest_concept-rebuilder_holographic.md
        │
        ├──────────► 🎬 考前大複習，想把細節串成故事？
        │           ➜ digest_storyline-curator.md
        │
        └──────────► 💡 讀得很枯燥，想要同儕心得與挑戰提問？
                    ➜ digest_peer-insight.md
```

---

## 📚 提示詞分類導覽

### 1. 知識消化與文件處理 (Document Digestion)
用於將大量原始資料轉化為結構化知識。

| 檔案 | 角色稱號 | 核心用途 | 適用情境 |
| :--- | :--- | :--- | :--- |
| **[digest_storyline-curator.md](./digest_storyline-curator.md)** | 故事串聯策展師 | 逐頁覆蓋、強調前後關聯與敘事線。 | 考前快速總複習、將講義串成教材。 |
| **[digest_concept-rebuilder_holographic.md](./digest_concept-rebuilder_holographic.md)** | 全息概念重建師 | 原子級拆解、圖表翻譯、生活化比喻。 | 深度學習難懂章節、重新建構核心概念。 |
| **[digest_peer-insight.md](./digest_peer-insight.md)** | 同儕洞察教練 | 第三人稱觀點、心得分享、質性提問。 | 激發思考興趣、從不同視角檢視內容。 |
| **[digest_document-shredder_progressive.md](./digest_document-shredder_progressive.md)** | 分段深潛導師 | **分段閱讀器**：先地圖後拆解，突破 Token 限制。 | 面對極厚（100頁+）或極艱澀的專業文獻。 |

### 2. 互動式學科教練 (Interactive Subject Coaching)
用於針對特定問題進行深度解答、解題或研究引導。

| 檔案 | 名稱 | 核心功能 | 適用情境 |
| :--- | :--- | :--- | :--- |
| **[coach_exam-consultant_holographic.md](./coach_exam-consultant_holographic.md)** | 全息教材考題教練 | **答題器**：找證據、分析選項、理科運算與協議圖繪製。 | 準備考古題、練習作業題，展現 LaTeX 計算細節與證據溯源。 |
| **[coach_research-advisor.md](./coach_research-advisor.md)** | 研究顧問助理 | **提案引導**：蘇格拉底式提問、研究動機與 SOTA 查核。 | 撰寫期末報告提案、碩博士論文研究開發階段。 |

### 3. 通用助理與開發工具 (Utilities)

| 檔案 | 說明 | 適用情境 |
| :--- | :--- | :--- |
| **[util_chat-assistants.md](./util_chat-assistants.md)** | 包含喵大人、狐小健、林老師等角色，以及 Git Commit 自動生成器。 | 日常對話趣味性、Git 提交流程自動化。 |

### 4. 元提示詞指南 (Meta-Prompting)

| 檔案 | 說明 | 適用情境 |
| :--- | :--- | :--- |
| **[meta_prompt-design.md](./meta_prompt-design.md)** | 提示詞設計的最佳實踐與規範。 | 當你需要自己設計或修改系統提示詞時的參考手冊。 |

---

## ⚡ 核心守則 (Global Guardrails)
所有專業角色皆受以下「天條」約束：
1. **No Hallucination**: 禁止捏造數據與引用。
2. **Pedagogical Logic**: 非僅給答案，而是透過深度解析引導學習。
3. **Depth Mandate**: 寧可詳細論述也不可點到為止，禁止暗示性跳過，所有細節必須當場展開。
4. **Traditional Chinese**: 全程繁體中文輸出。

---
**最後更新：2026-04-11** (簡化變體命名、全面修復為相對路徑超連結 `./`)
