---
category: workflow
purpose: 一個 commit 只做一件事
combine: 可與任何 rule 搭配
---

# 原子化提交 (Atomic Commits)

> 一段可以貼進 CLAUDE.md / AGENTS.md 的行為規則。

## 可貼上片段

提交規則：
1. 一個 commit = 一個邏輯變更，能用一句話說清楚 — 方便 git bisect 和 code review。
2. 改名用 `git mv`，禁止刪除再新增，否則 git 歷史斷裂。
3. 程式碼還在（搬移）→ 一個 commit；程式碼消失（刪除）→ 另一個。
4. Commit 前跑 `git status`，確認沒有混入不相關變更。
5. Commit 訊息 header 用 `type(scope): 一句話`，不用廢話。

---

## 完整說明

### 核心心法

**一個 commit = 一件事。如果沒辦法用一句話說完它做了什麼，它就不該是一個 commit。**

## 為什麼需要這條規則

你可能覺得「反正都是改同一個檔案」，就把所有變更塞進同一個 commit。但當你 six 個月後要找「那次修復 login bug 的變更」，你得在一個巨大的 diff 裡大海撈針。

更糟糕的是 git bisect — 如果一個 commit 裡混了三個不相關的變更，當你二分搜尋找 bug 時，你永遠沒辦法精確定位到是哪個變更引入的問題。

原子化提交讓你的 git 歷史**可讀、可追溯、可回滾**。

## 你該遵循的原則

### 1. 一個 commit = 一個邏輯變更

判斷標準：這個 commit 能不能用一句話說清楚？

- ✅ 「修復登入時的 null pointer exception」
- ✅ 「將 UserHelper 拆分到獨立檔案」
- ❌ 「修復登入 bug + 更新 README + 重命名 utils」

如果一個 commit 裡有兩個不相關的目的，拆成兩個。

### 2. 改名 ≠ 刪除

- 改名必須用 `git mv`，不要刪除舊檔案再新增同名檔案
- 這樣 git 才能正確追蹤檔案的歷史

### 3. 移動 vs 刪除的判斷

問自己：**程式碼在變更後還在嗎？**

- 還在（只是搬到別的地方）→ 一個 commit（move/extract）
- 不在了（真的被刪掉）→ 另一個 commit（delete）
- 一個檔案改名 + 改了內容 → 兩個 commit（先 rename，再 modify）

### 4. Commit 前的最後一步

執行 commit 之前，跑一下 `git status`：
- 確認沒有不小心暫存的垃圾檔案
- 確認這次 commit 的範圍正確
- 確認沒有混入不相關的變更

### 5. Commit 訊息要有意義

好的 commit 訊息讓人不用看 diff 就知道發生了什麼：
- Header：`type(scope): 一句話說清楚做了什麼`
- Body：用編號列表列出具體改了什麼（英文）
- 不要用「update」、「fix bug」這種廢話當 header
