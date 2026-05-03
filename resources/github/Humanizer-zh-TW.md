# Humanizer-zh-TW: AI 寫作人性化工具（繁體中文版）

## 安裝 (Agent Skills)
### 方式一：透過 npx add-skill 安裝（推薦）
```bash
npx add-skill kevintsai1202/Humanizer-zh-TW
```

### 方式二：安裝到特定代理程式
- **Antigravity**:
```bash
npx add-skill kevintsai1202/Humanizer-zh-TW -a antigravity -g -y
```
- **Claude Code**:
```bash
npx add-skill kevintsai1202/Humanizer-zh-TW -a claude-code -g -y
```
- **Cursor / Roo Code**: 支援透過 `add-skill` 工具快速部署。

## 使用
在對話中呼叫：
1. `/humanizer-zh-tw 請幫我人性化以下文字：[貼上內容]`
2. `請用 humanizer 幫我改寫這段話，讓它更自然。`

## 核心功能：24 種 AI 寫作模式辨識
- **內容模式**：過度強調意義、遺產、提綱式展望。
- **語言模式**：AI 常用詞（此外、佈局、關鍵角色）、否定式排比。
- **風格模式**：破折號/粗體過度使用、標題首字母大寫。
- **交流模式**：諂媚語氣、通用積極結論。

---
*來源: [kevintsai1202/Humanizer-zh-TW](https://github.com/kevintsai1202/Humanizer-zh-TW)*
