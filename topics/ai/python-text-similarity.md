# 使用 Python 計算中文文本相似度

本文整理自一篇關於使用 `sentence-transformers` 函式庫計算中文文本相似度的教學。

## 核心概念

目標是透過比較兩個句子的語義來判斷它們的相似程度，而非僅僅是字面上的比較。

- **核心工具**: `sentence-transformers` 函式庫。
- **推薦模型**: `paraphrase-multilingual-MiniLM-L12-v2`。這是一個輕量、高效能且支援多種語言（包含中文）的預訓練模型。
- **計算方法**:
    1.  **文本向量化 (Embeddings)**: 使用模型將句子轉換成一個固定維度（此模型為 384 維）的數字向量。這個向量代表了句子的語義資訊。
    2.  **相似度計算**: 使用「餘弦相似度 (Cosine Similarity)」來計算兩個句子向量之間的夾角。結果越接近 1，表示語義越相似。

## 實作步驟

### 1. 安裝函式庫

```bash
pip install sentence-transformers
```

### 2. 撰寫 Python 程式碼

```python
from sentence_transformers import SentenceTransformer
from sentence_transformers.util import cos_sim

# 載入預訓練模型
# 注意：第一次執行會自動下載模型，可能會需要一些時間
model = SentenceTransformer('paraphrase-multilingual-MiniLM-L12-v2')

# 待比較的句子
sentences1 = ['如何更換花唄綁定銀行卡']
sentences2 = ['花唄更改綁定銀行卡', '我的花唄額度是多少']

# 將句子編碼成向量
embeddings1 = model.encode(sentences1)
embeddings2 = model.encode(sentences2)

# 計算餘弦相似度
cosine_scores = cos_sim(embeddings1, embeddings2)

# 輸出結果
# cosine_scores[0][0] 是 '如何更換花唄綁定銀行卡' 和 '花唄更改綁定銀行卡' 的相似度
# cosine_scores[0][1] 是 '如何更換花唄綁定銀行卡' 和 '我的花唄額度是多少' 的相似度
print(f"'{sentences1[0]}' vs '{sentences2[0]}': {cosine_scores[0][0]:.4f}")
print(f"'{sentences1[0]}' vs '{sentences2[1]}': {cosine_scores[0][1]:.4f}")
```

### 3. 處理模型下載問題 (選用)

在特定網路環境下（如中國大陸），直接從 Hugging Face 下載模型可能會失敗。解決方法如下：

1.  **手動下載**: 從 [Sentence-Transformers 模型鏡像站](https://public.ukp.informatik.tu-darmstadt.de/reimers/sentence-transformers/v0.2/) 找到並下載 `paraphrase-multilingual-MiniLM-L12-v2.zip`。
2.  **解壓縮**: 將下載的檔案解壓縮到一個資料夾。
3.  **本地載入**: 在程式碼中，將模型名稱替換為解壓縮後的本地資料夾路徑。

```python
# model = SentenceTransformer('paraphrase-multilingual-MiniLM-L12-v2')
# 改為以下方式：
model = SentenceTransformer('C:/path/to/your/model/paraphrase-multilingual-MiniLM-L12-v2')
```

## 相關套件

-   `text2vec`: 另一個文本處理套件，其底層也使用了 `sentence-transformers`。

## 參考資料

-   [sentence-transformers GitHub](https://github.com/UKPLab/sentence-transformers)
-   [text2vec GitHub](https://github.com/shibing624/text2vec)
