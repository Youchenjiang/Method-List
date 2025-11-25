# System Prompts 系統提示詞集合

此資料夾存放各種 AI 助手的系統提示詞（System Prompts），用於定義 AI 的角色、行為準則與回應風格。

## 📋 命名規則

檔案命名格式：`{角色名稱}_{變體類型}.md`（若同一檔需容納多個 Profile，可使用 `_profiles` 後綴，例如 `data-organization-expert_profiles.md`）

- **角色名稱**：描述 AI 扮演的角色（例如：data-organization-expert、teacher）
- **變體類型**：同一角色的不同版本或風格（例如：base、detailed、concise、experimental）

### 範例
- `data-organization-expert_base.md` - 資料整理專家的基礎版本
- `data-organization-expert_detailed.md` - 資料整理專家的詳細版本
- `teacher_base.md` - 教師角色的基礎版本
- `teacher_casual.md` - 教師角色的輕鬆版本

## 📚 現有提示詞

### 資料整理專家 (Data Organization Expert)

| 檔案 | 版本 | 說明 | 適用情境 |
|------|------|------|----------|
| `data-organization-expert_profiles.md` | v4.0 | 單檔整合三個 Profile（故事串聯策展師 / 全息概念重建師 + Turbo / 同儕洞察教練），並在流程內建動態模組互相補充 | 從考前複習、深度拆解到第三人稱觀點都可以在一次輸出中完成 |

### 聊天助理 & 實用提示詞 (Chat Assistants & Utilities)

| 檔案 | 說明 | 適用情境 |
|------|------|----------|
| `chat-assistants_collection.md` | 各種實用 AI 提示詞集合，包含角色扮演、工作輔助等 | 需要特定風格的聊天助理或開發工具輔助時使用 |

## 💡 使用建議

1. **選擇適合的版本**：根據任務需求選擇對應的變體
2. **保留所有版本**：不要刪除舊版本，方便日後對比和回溯
3. **記錄差異**：建立新變體時，在此 README 中記錄其特點與用途
4. **實驗性版本**：可以使用 `_experimental` 後綴來標記正在測試的版本

## 🔄 版本演進追蹤

如需記錄某個角色提示詞的演進歷史，建議在對應的檔案中加入版本資訊區塊：

```markdown
## 版本資訊
- 創建日期: YYYY-MM-DD
- 最後更新: YYYY-MM-DD
- 版本: v1.0
- 變更記錄: [簡述主要變更]
```

## 📝 新增提示詞指南

當您要新增一個新的系統提示詞時：

1. 確定角色名稱和變體類型
2. 建立對應的 `.md` 檔案
3. 在本 README 的「現有提示詞」區塊中更新表格
4. 在檔案末尾加入版本資訊

---

**最後更新：2025-11-25**
