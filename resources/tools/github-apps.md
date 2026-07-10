# GitHub Apps 參考

本文件收錄實用的 GitHub Marketplace Apps，安裝到倉庫後自動運行，無需本地安裝。

---

## 🔍 AI 程式碼審查 (PR Review)

| 工具 | 連結 | 說明 |
| :--- | :--- | :--- |
| **Pull Assistant** | [GitHub Marketplace](https://github.com/marketplace/pull-assistant) | 分析 PR 並建議最佳審查方式（commit-by-commit 或全量），開源免費 |
| **Astronuts** | [GitHub Marketplace](https://github.com/marketplace/astronuts-app) | AI 逐行審查 + 靜態分析 + 變更摘要，支援 10 種語言，免費 |
| **Sourcery AI** | [sourcery.ai](https://sourcery.ai) | 即時 PR 審查 + 200+ Python 規則 + IDE 整合（VS Code/JetBrains），免費層級 |
| **LlamaPReview** | [GitHub App](https://github.com/apps/llamapreview) | 證據導向 AI 審查，上下文感知（非僅 diff），多語言，完全免費 |

---

## 🔐 安全掃描 (Security Scanning)

> ⚠️ 以下為 GitHub Actions，需在 `.github/workflows/` 下建立 YAML 檔案才能啟用，與上方直接安裝的 GitHub Apps 不同。

| 工具 | 連結 | 說明 |
| :--- | :--- | :--- |
| **TruffleHog** | [GitHub Action](https://github.com/marketplace/actions/trufflehog-oss) | 掃描 Git/Docker/S3 等來源的洩漏憑證，可驗證密鑰是否有效，支援 700+ 憑證類型 |

```yaml
# .github/workflows/trufflehog.yml
name: Secret Scanning
on: [push, pull_request]
jobs:
  trufflehog:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - uses: trufflesecurity/trufflehog@main
        with:
          extra_args: --results=verified,unknown
```

---

**最後更新：2026-07-09**
