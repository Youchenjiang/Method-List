# 如何強制 Git 追蹤檔案或資料夾的大小寫變更

在 Windows 或 macOS 等大小寫不敏感 (Case-Insensitive) 的檔案系統上，開發者常會遇到一個棘手的問題：當你只改變一個檔案或資料夾的大小寫時（例如，將 `readme.md` 改為 `README.md`，或將 `src` 改為 `SRC`），Git 可能無法偵測到這個變更。

這篇文章將說明這個問題的根本原因，並提供一個最可靠的解決方案。

## 什麼是問題的根源？

問題在於 Git 的一個核心設定：`core.ignorecase`。

在大小寫不敏感的作業系統上，這個設定預設為 `true`。這意味著 Git 會忽略檔名的大小寫差異，將 `File.txt` 和 `file.txt` 視為同一個檔案。因此，當你只修改大小寫時，`git status` 不會顯示任何變更，你也無法將這個「不存在的」變更提交上去。

這會導致本地檔案系統和遠端 GitHub 倉庫之間的狀態不一致，進而引發連結失效等問題。

## 解決方案：使用 `git rm --cached`

雖然 `git mv` 是官方推薦的重命名工具，但在處理純大小寫變更時，它有時會因為系統的混淆而出錯。一個更穩定、更明確的方法是透過「先從索引中移除，再重新加入」的兩步驟來完成。

這個方法不會刪除你的本地檔案，請放心使用。

### 操作步驟

假設我們要將資料夾 `data` 重命名為 `Data`：

**步驟 1：從 Git 索引中移除舊名稱**

執行以下指令，將資料夾（或檔案）從 Git 的追蹤清單中移除。`--cached` 參數是關鍵，它保證了只操作索引，而不會動到你本地的實際檔案。

```bash
# 對於資料夾，需要加上 -r 參數
git rm -r --cached data

# 對於單一檔案
git rm --cached readme.md
```
> **注意**：這裡的 `data` 或 `readme.md` 必須是 Git 索引中記錄的「舊」的大小寫名稱。

**步驟 2：將新名稱重新加入索引**

現在，你的檔案在本地依然存在，只是 Git 暫時「假裝」不認識它了。接下來，我們用 `git add` 把它重新加回來。Git 會以檔案系統中「新」的大小寫來記錄它。

```bash
git add Data
git add README.md
```

**步驟 3：檢查狀態並提交**

執行 `git status`，你會看到 Git 現在明確地將這個變更識別為一次「重命名」(rename)。

```
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    data/file.txt -> Data/file.txt
```

確認無誤後，即可正常提交 (`git commit`)。這個變更現在會被永久記錄下來，並能成功推送到遠端倉庫。

---

這個 `git rm --cached` 的技巧是處理 Git 在跨平台（特別是 Windows/macOS 與 Linux 之間）協作時，因大小寫問題導致各種奇怪狀況的萬用解方。
