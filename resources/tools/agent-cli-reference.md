# AI Agent CLI 設定與路徑指南 (AI Agent CLI Configurations)

本文件記錄本機上各個 AI Agent / CLI 工具的設定檔（MCP）、指令檔（Instructions）與相關機制的實體路徑。為便於跨設備使用與快速存取，路徑均採用 **Windows 檔案總管及命令列相容的環境變數格式**。

---

## 🛠️ Agent 核心配置對照表

您可直接複製以下路徑並貼入 **Windows 檔案總管網址列** 或 **「執行」視窗 (Win + R)** 直接開啟對應檔案：

| Agent / CLI 名稱 | 檔案總管相容路徑 (可直接複製貼上) | 核心功能 | 快速開啟資料夾指令 (於 CMD/PS 執行) |
| :--- | :--- | :--- | :--- |
| **Codex CLI** | `%USERPROFILE%\.codex\config.toml` | MCP 伺服器與工具連接設定 | `explorer %USERPROFILE%\.codex` |
| | `%USERPROFILE%\.codex\AGENTS.md` | Codex 專屬行為與指令檔 | |
| **Gemini CLI** | `%USERPROFILE%\.gemini\settings.json` | 全域 MCP 連線與 API 設定 | `explorer %USERPROFILE%\.gemini` |
| | `%USERPROFILE%\.gemini\GEMINI.md` | Gemini 全域指令與偏好 | |
| **Antigravity** | `%USERPROFILE%\.gemini\antigravity\mcp_config.json` | 專案模式的專用 MCP 設定 | `explorer %USERPROFILE%\.gemini\antigravity` |
| | `%USERPROFILE%\.gemini\antigravity\AGENTS.md` | Antigravity 核心 Pair 準則 | |

> 📌 **說明**：`%USERPROFILE%` 在 Windows 系統中會自動解析為使用者的家目錄（本機路徑：`C:\Users\g1014308\`）。

---

## ⚙️ 進階機制說明

### Gemini CLI - BeforeTool Hook
* **作用**：在執行工具前觸發。
* **主要用途**：做為行為提醒機制（如：提醒優先使用 MCP 關係圖工具而非傳統 Grep 搜尋）。

---

## 💡 使用建議與維護
1. **修改生效**: 這些設定均位於使用者家目錄下，若修改了對應的 `.md`、`.json` 或 `.toml` 檔案，重啟對應的 CLI 或 Agent 即可生效。
2. **跨設備相容**: 由於使用了 `%USERPROFILE%` 環境變數，此設定指南無需修改使用者名稱（如 `g1014308`），即可在任何 Windows 電腦上直接使用。
