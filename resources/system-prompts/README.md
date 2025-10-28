# System Prompts 系統提示詞集合

此資料夾存放各種 AI 助手的系統提示詞（System Prompts），用於定義 AI 的角色、行為準則與回應風格。

## 📋 命名規則

檔案命名格式：`{角色名稱}_{變體類型}.md`

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
| `data-organization-expert_simple.md` | v1.0 | 簡化版本，著重教學式風格與自我檢查 | 快速整理簡報、課堂筆記等較簡單的內容 |
| `data-organization-expert_detailed.md` | v2.0 | 詳細版本，包含完整的六大核心執行策略 | 需要全面、系統化整理複雜資料時使用 |
| `data-organization-expert_accessible.md` | v3.0 | 無障礙版本，新增螢幕閱讀器相容規範 | 需要產出無障礙報告或服務視障用戶時使用 |

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

**最後更新：2025-10-29**
