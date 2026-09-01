# AI驅動教育環境下的特徵選擇方法比較研究

# ABSTRACT
現代教育經過深刻的典範轉變，從傳統面對面教師主導教學轉變為人工智慧的個人化與互動式學習，而生成式人工智慧（GenAI）進一步的興起重塑學生的日常學習行為和學業表現。產生了大規模且多維度的學習資料，使學習表現預測成為識別高風險學習者與針對性教育干預的關鍵工具。然而這些模型實際價值受到特徵選擇（FS）使用方法不一致的限制，且缺乏針對人工智慧驅動的教育環境的系統性比較，特別是平衡教育人士關注的準確性與可解釋性。本研究對三種主流的fs 方法系統性研究，說明他們在不同計算限制下的性能差異，為機器學習在教育上的應用提供實用能可解釋的指引。
# 1. Introduction
## 1.1 Background and Motivation
傳統的教師主導、單向的面授教學已演變為 AI 支援的互動式和個人化學習生態。早期的教育人工智慧（AIEd）主要遵循教師指導，其中智慧教學系統（ITS）控制學習進度 [1]。隨著技術的進步，適應性學習平台被廣泛用於根據學生個人的需求量身定制內容 [2]，最終將重點放在即時學習者回饋上 [3]。
最近GenAI的爆發引發了第二次模式轉變，從系統主導的平台轉向學生主導的、高度自主的AI互動。現代學生已有用ai工具學習的習慣，多了新的特徵，例如提示頻率、AI依賴度和使用目的。有趣的是，最近的實證研究證實，廣泛使用GenAI並不會直接提升學業成績：近一半使用的學生說，儘管感覺效率有所提高，但成績沒有顯著提升，也就是過度依賴Ai與學業成績下降和自主學習能力減弱有關 [4],[5] 。AI工具使用與實際學習成果之間的這種脫節，使評估學生學業變得更複雜，並強調了對可解釋預測分析的需求，凸顯了FS在教育分析中的關鍵作用。
雖然機器學習（ML）已成為學生績效預測和高危學生識別的核心工具，但往往受到這些模型「黑箱」性質的阻礙。會因為有限的可解釋性限制了現實應用，教育工作者需要透明度來信任工具，也需要確保結果偏差較小[6]。而現有研究大多使用一般教育資料對FS方法進行基本比較，很少以AI驅動的學習環境為中心，或在統一且多條件下做FS的比較。
此外，每種主流的FS方法都有充分記載的局限性：Filter methods計算效率高，但通常忽略特徵與分類器之間的交互以及特徵之間的依賴關係[7]；Wrapper methods通過捕獲特徵交互來提供更強的預測性能，但計算成本極高，並面臨嚴重的過擬合風險[8]；而Embedded methods雖然在效率和準確性之間取得了平衡，但在結構上與特定的基礎分類器相關聯，限制了它們的通用性[9]。
本研究在AI驅動的教育環境中系統地比較了過濾法、包裝法和嵌入法這三種FS方法。為了確保現實世界的可解釋性能實踐，排除特徵提取技術（例如PCA），以保留學習特徵的原始含義。並且與完全不透明的深度神經網路相比，我們優先選擇適度透明的基於樹的分類器。在不同的特徵數條件下評估這些方法，以平衡預測能力、效率。
## 1.2 Contributions
1. FS的系統性多條件評估：本研究針對人工智慧驅動的教育場景，對過濾、包裝、嵌入進行全面多條件比較，彌補關鍵缺口。在三種限制條件（無限制特徵數量、嚴格最小值和指定閾值）下評估這些方法，確認它們在資源受限的環境下性能、計算效率和穩定性。
2. 領域特定的特徵發現與實用指導：除了性能比較，本研究強調教育可解釋性。通過分析三種方法所選擇的特徵之間的交集和重疊，判斷出讓學生表現優良的核心、高影響力學習行為。為教育工作者和研究人員提供了有證據的指南。
## 1.3 Research Questions
本研究由四個核心研究問題引導：
- RQ1：在不受限制的計算條件下，過濾法（Filter）、包裝法（Wrapper）和嵌入法（Embedded）在預測性能、最佳特徵數量和特徵重疊方面比較結果如何？
- RQ2：當所有三種方法都被迫在極端特徵壓縮下運行（即限制在相同的最小特徵數量）時，會對模型性能產生怎樣的影響？
- RQ3：在固定的特徵數量約束下（測試多個k閾值），哪種方法能最好地保持預測穩定性，使其在資源有限的場景中達到最優？
- RQ4：從所有三種方法選擇的特徵交集中共識出哪些核心且影響力大的學習行為？這些行為如何為教育干預提供依據？
本研究的其餘部分組織如下：第2節回顧有關特徵選擇和教育數據分析的相關研究；第3節概述研究方法；第4節介紹實驗設計和結果；第5節總結研究並討論未來工作。
# 2 RELATED WORK
## 2.2 Student Learning Performance with AI
學習成效評估是教育資料探勘(EDM)與學習分析(LA)的主要議題，主要目標即透過系統性的數據分析，即早識別高學業風險的學生，提供教育人士介入的策略。傳統預測模型高度依賴靜態學業資料與統計，根據 Alalawi 等人 **[6]** 針對 2010 至 2022 年間 162 篇機器學習預測學生成績的系統性文獻回顧指出，過去十年的研究極度仰賴傳統學習管理系統（LMS）的後台數據與過往成績。然而，這篇回顧也揭漏了兩大局限：1.僅有約30%研究採用FS技術來優化模型；2.多數預測採用「黑箱模型」，嚴重阻礙教師理解背後邏輯，進而導致他們難以制定有效的教學干預策略。

而隨著數位學習環境的演進，單一LMS的資料無法全面反映學習全貌，Trakunphutthirak 與 Lee **[12]** 的研究證實，結合數位足跡與網路使用行為能更精準的捕捉學生時間管理與自我規劃能力。他們的研究同時也強調採用可解釋性的樹狀模型能幫助教育人士理解學生陷入高風險的具體行為路徑 **[12]** 。近期GenAI發展更顛覆學生的行為模式，引入了新的特徵。Uppal 與 Hajian **[13]** 在 2025 年的最新研究中指出，儘管ChatGPT的輔助效用普遍被認可，但「對AI工具的過度依賴AI dependency與 academic procrastination」呈現顯著的正相關，長期過度依賴會削弱他們自主思考與批判能力 **[13]** 。也就意味著較好的學業預測模型應該將 AI 使用頻率（Prompts per week）、依賴度及生成內容比例等新型動態特徵納入考量。

雖然對學生的行為數據已從傳統靜態lms指標轉為複雜且多維的生成式ai互動資料，現有FS與預測文獻出現了明顯斷層，如停留在舊有資料集探討FS[6] 與針對GenAI行為基礎的問卷與統計分析[13]，仍缺乏針對AI新環境的新興特徵，進行Filter、Wrapper 與 Embedded 三大特徵選取流派的系統性比較。因此重新評估並找出最兼顧高預測力與高教育解釋性的FS方法是當前亟待解決的關鍵挑戰
# 3. METHODOLOGY

## 3.1 Method Overview
本研究旨在探討並比較在有生成式AI的輔助學習下，不同FS方法對學生學習成效預測的影響。整體研究流程主要分為四個階段，如圖?所示：1. 對資料集中的原始學生學習與AI使用資料分別做資料清洗與前處理；2.分別套用 filter、wrapper與 embedded三種 fs 方法，在不同條件下擷取關鍵特徵；3.將篩選出來的特徵輸入至Decision Tree 分類中進行訓練；4. 透過多項評估指標比較各方法的預測效能與特徵穩定性。
## 3.2 Data Analysis and Preprocessing
為了確保機器學習模型能夠有效學習，我們對原始資料集進行了嚴謹的特徵工程與前處理：
- **Target Variable Definition**: 本研究的預測目標屬於二元分類任務，選定passed欄位作為目標變數(標籤y)，來預測學生是否會通過該課程。我們在訓練過程中，意外發現了會導致模型產生虛假的高準確率的Target Leakage情況，在排查後確定是資料集中的事後變數所造成(即 `final_score` 與 `performance_category`欄位)，如圖?所示，當模型可以直接以`final_score`進行判斷時，會發生Target Leakage，同時伴隨著所有評估指標都失效(分數大於60即可100%準確預測結果)。另外我們也將無預測價值的編號(`student_id`)一齊移除。
- **Missing Value Handling**: 為了維持原始資料特徵的真實分布，避免imputation 會產生人為誤差，在樣本數足夠多的情況下，我們直接採取Listwise deletion，將帶缺失值的資料列移除。
- **Categorical Feature Encoding**: 對於非數值型變數，根據該變數特性採取以下不同的編碼策略。1. 對順序性質的`grade_level`，轉成Ordinal Encoding；2. 對多重標籤特性的`ai_tools_used`，進行個別的One-Hot Encoding；3. 對其他變數統一採取丟棄首位(`drop_first=True`)的One-Hot Encoding方式，以消除Dummy variable trap引起的共線性問題。
- **Feature Scaling**: 本研究所有特徵選取與最終分類皆採用Tree-based algorithms，而決策樹的分支邏輯依賴特徵的相對排序而非絕對值大小，因此特徵具有Scale-invariant。基於這個特性，本實驗直接省略Standardization 或 Normalization ，完整保留對原始資料的解釋性
# 3.3 Feature Selection
本研究實作並比較了三種主流的FS流派，分別在相同隨機種子(`random_state=42`)的狀態下進行，以確保實驗的可重現性：
- **Filter**: 採用`SelectKBest` 演算法搭配MI 作為評分標準。MI 能夠捕捉特徵與目標變數之間複雜的非線性關係，藉此計算出每個特徵的獨立重要性分數，並篩選出得分最高的 $k$ 個特徵。
- **Wrapper**: 採用RFECV，我們以基礎DT(未設定`entropy` 跟 `class_weight`)作為基底模型（Base Estimator），並設定 5 折交叉驗證（$k=5$ fold CV）。為了因應教育數據中可能出現的類別不平衡問題，我們指定 `F1-score` 作為優化與評分標準（scoring metric），演算法會反覆訓練並剔除最不重要的特徵，直到找出能使 F1-score 最大化的最佳特徵組合。
- **Embedded：** 利用 `SelectFromModel` 模組，直接將特徵選取嵌入至決策樹模型的訓練過程中。我們透過提取模型內部的 `feature_importances_` 屬性來評估變數貢獻度，並將篩選閾值（Threshold）設定為特徵重要性的平均值，自動保留對節點純度提升有顯著貢獻的特徵。
# 3.4 Training Classifier
- **Train/Test Split**： 處理完畢的資料集以 80% 作為訓練集，20% 作為測試集；設定固定的隨機種子（`seed=42`）；再加上Stratified sampling機制，確保不同特徵選取方法所面對的測試基準完全一致。
- **Classifier Settings**： 為了聚焦於探討「特徵選取」本身的影響力，並最大化教育現場的「模型可解釋性」，我們統一採用決策樹分類器（Decision Tree Classifier）作為最終的成效評估模型。超參數分別設定如下：分支準則採用資訊熵（`criterion='entropy'`）；特別啟用類別權重平衡（`class_weight='balanced'`），強制模型在訓練時對少數類別（例如未通過的高風險學生）給予較高的關注度，從而提高預測的實用價值。
# 3.5 Evaluate Features Selection Performance
1. Predictive Performance Metrics: EDM中，單純依賴Accuracy往往會掩蓋模型對特定類別學生的預測盲點。因此我們綜合使用四項指標，以「通過課程」(Positive class, label=1)來全面評估模型效能：
	- **Accuracy (準確率):** 衡量在所有樣本中，模型正確預測的整體比例，為模型效能提供最直觀的基準評估。
	- **Precision：** 衡量模型預測為「通過」的學生中，多少比例是真正的通過。
	- **Recall：** 衡量在所有「真正通過」的學生中，模型成功抓出了多少比例。
	- **F1-Score：** 面對及格與不及格人數可能不平衡的學生資料，提供比單一準確率更客觀、具綜合性的模型效能評估。
2. Feature Stability and Overlap Metric: 
	- **Jaccard Similarity:** 代表干預該特徵子集的價值
# 4. 
# 5. DISCUSSION
## 5.1 Real-world Practices in Education
1. 實驗一和實驗三反覆出現的三個核心特徵`last_exam_score`、`assignment_scores_avg`、`concept_understanding_score`，證明傳統學業表現依舊是及格與否的關鍵預測指標
2. wrapper 和 embedded保留的 `ai_generated_content_percentage` 以及 `ai_prompts_per_week` 兩個交互和互補的特徵，也與文獻回顧中提到的「過度依賴 AI 可能導致學習能力下降」的確有關，我們可以考慮以3~5個特徵做第一層的快速篩檢，針對需要特別關注的學生，再加入第二層的AI 使用行為特徵相關輔助判斷，以兼顧成本與準確性。
## 5.2 Research Limitations
本研究有以下限制。第一，資料來源為單一Kaggle 開放資料集，尚未以跨學校、課程、地區等不同資料進行驗證；第二，資料標籤高度不平衡(pass占多數)，雖使用class_weight，依舊有可能影響少數類別的判斷準確性；第三，實驗二的bottleneck設計機制在本資料集上幾乎不起作用，導致跟實驗1的設定幾乎一致；第四，在本研究僅使用決策樹，可能無法反映特徵在其他複雜模型上。第五，本研究以 Jaccard 衡量特徵集合重疊，能反映一致性，但無法反映特徵排序與權重差異
Future Research:
1. 進行多資料集與跨課程的外部驗證，檢驗特徵穩定性與可遷移性。
2. 在特徵穩定性上加入 rank-based 指標（如 Kendall tau）與重要性一致性分析。
3. 比較 Decision Tree 與 Random Forest、XGBoost、Logistic Regression 等模型在「效能-可解釋性」間的折衷。
4. 將預測結果導入實際教學干預流程，評估對學習成效與留存率的真實提升。

# 6. CONCLUSION
結果顯示，1. 當資源充足時，三種方法展現了極高的共識，且僅用 3 個特徵就能超越使用全部特徵的Baseline，證明適當特徵選擇可以提升F1-Score；2. 在固定特徵數量 (Fixed $k$) 的限制下，**Embedded 方法**展現出最高的穩定性，並在 $k=7$ 時取得了最佳的預測效能；3. Filter 方法雖然未能在多數設定中取得最佳成績，但整體表現與最佳模型相近，證明其作為「低運算成本」的基準方法仍具有高度競爭力。

# 已參考文獻
1. Fan, O., & Jiao, P. (2021). Artificial intelligence in education: The three paradigms. _Comput. Educ. Artif. Intell._, 2, 100020. https://doi.org/10.1016/j.caeai.2021.100020.
2. Strielkowski, W., Grebennikova, V., Lisovskiy, A., Rakhimova, G., & Vasileva, T. (2024). AI‐driven adaptive learning for sustainable educational transformation. Sustainable Development. https://doi.org/10.1002/sd.3221.
3. Ouyang, F., Wu, M., Zheng, L. _et al._ Integration of artificial intelligence performance prediction and learning analytics to improve student learning in online engineering course. _Int J Educ Technol High Educ_ **20**, 4 (2023). https://doi.org/10.1186/s41239-022-00372-4
4. Fan, L., Deng, K. & Liu, F. Educational impacts of generative artificial intelligence on learning and performance of engineering students in China. _Sci Rep_ **15**, 26521 (2025). https://doi.org/10.1038/s41598-025-06930-w
5. Revesai, Z. (2025). Generative AI dependency: the emerging academic crisis and its impact on student performance—a case study of a university in Zimbabwe. _Cogent Education_, _12_(1). https://doi.org/10.1080/2331186X.2025.2549787
6. Alalawi K, Athauda R, Chiong R. Contextualizing the current state of research on the use of machine learning for student performance prediction: A systematic literature review. Engineering Reports. 2023;5(12):e12699. doi: 10.1002/eng2.12699
7. Pudjihartono N, Fadason T, Kempa-Liehr AW and O'Sullivan JM (2022) A Review of Feature Selection Methods for Machine Learning-Based Disease Risk Prediction. Front. Bioinform. 2:927312. doi: 10.3389/fbinf.2022.927312
8. Jain R, Xu W. Artificial Intelligence based wrapper for high dimensional feature selection. BMC Bioinformatics. 2023 Oct 18;24(1):392. doi: 10.1186/s12859-023-05502-x. PMID: 37853338; PMCID: PMC10585895.
9. Figueroa Barraza J, López Droguett E, Martins MR. Towards Interpretable Deep Learning: A Feature Selection Framework for Prognostics and Health Management Using Deep Neural Networks. Sensors (Basel). 2021 Sep 1;21(17):5888. doi: 10.3390/s21175888. PMID: 34502778; PMCID: PMC8433983.
10. Basic Study
11. Dataset
12. Trakunphutthirak, R., & Lee, V. C. S. (2022). Application of Educational Data Mining Approach for Student Academic Performance Prediction Using Progressive Temporal Data. _Journal of Educational Computing Research_, _60_(3), 742-776.
13. Uppal, K., & Hajian, S. (2025). Students’ perceptions of ChatGPT in higher education: A study of academic enhancement, procrastination, and ethical concerns. _European Journal of Educational Research, 14_(1), 199-211. https://doi.org/10.12973/eu-jer.14.1.199
## 舊寫法


近年人工智慧與數位教育技術普及，推動學生學習型態發生關鍵典範轉移，逐步脫離傳統以教師為核心的實體單向授課模式，朝AI驅動的互動式、個人化學習場域演進。早期教育人工智慧（AIEd）屬於**AI-directed, learner-as-recipient**範式，系統全權主導學習節奏與內容，學生處於被動接收狀態，常見的智慧家教系統即為此範式的典型應用[1]。隨技術發展，適應性學習平台逐步普及，此類系統可依學生的學習優劣勢、偏好調整教學內容與進度，有效提升課程及格率與學生留存率，實現永續教育轉型的核心價值[2]。而AIEd領域更前沿的發展，則聚焦AI成績預測模型與學習分析的整合，彌補傳統模型僅優化算法精度、忽視即時學習反饋的短板，進一步落實以學生為中心的學習路徑建構[3]。


近年來，隨著人工智慧技術與數位教育科技全面普及，全球教育場域的學習型態已產生深刻變革，逐步從「以教師為核心、課堂講授為主的單向實體教學模式」，轉向「由人工智慧技術支撐的互動式、個人化學習環境」，形成教育領域顯著的**學習型態典範轉移**。回溯教育人工智慧（Artificial Intelligence in Education, AIEd）的發展歷程，早期研究與應用多以系統為絕對主導，由人工智慧系統全權把控學習節奏、教學內容與活動設計，學生多處於被動接收的角色，接受系統給定的學習指引與教學任務；此一模式正是Fan與Jiao提出的AIEd三大範式分類中，**「AI-directed, learner-as-recipient」**的核心內涵，而當前廣泛應用的**智慧家教系統**，即屬於此一範式的典型應用類型[1]。

伴隨運算算力升級與學習分析技術成熟，人工智慧於教育場域的角色逐步轉型，從早期全權主導學習的控制者，轉為學習歷程的支撐者與協同者，智慧家教系統、學習風格偵測工具、適性化學習平台等基礎應用也隨之普及。此階段的AI驅動系統屬於**被動響應型適應性學習**，核心邏輯為系統針對學習者當下的線上行為、作答軌跡與互動數據即時蒐集分析，進而動態調整教材難度、內容呈現形式與基礎學習路徑，打破早期AIEd單向傳遞的侷限，建立系統與學習者的雙向互動協作模式。針對此類基礎適應性系統的長遠教育價值，Strielkowski等人於研究中明確指出，這類系統不僅能優化個體學習體驗，更能培育具備良好教育素養的群體，幫助學習者建立獨立思辨能力、做出理性學習與發展決策；而高素養學習群體反過來能推動可持續性教育實務優化與決策革新，帶動教育領域整體創新，最終回饋並完善整體教育體系，形成科技與教育共生的良性循環[2]。現階段這類基礎互動學習平台，更結合即時回饋、遊戲化設計與模擬教學情境，進一步提升學習參與度與內在動機，推動傳統齊一式講授，轉向兼顧個體差異的動態彈性教學流程。

在基礎適應性學習的技術積累之上，教育人工智慧（AIEd）領域朝著更精準、更以學習者為核心的方向突破，依託先進計算技術發展的**AI成績預測模型**，成為當下最具實踐價值的前沿方向，這也是與第二段基礎適配模式的核心差異所在。此類模型被廣泛應用於識別具掛科風險的學生、建構量身定制的學生中心學習路徑，同時輔助教師優化整體教學設計與課程開發，彌補傳統適應性系統僅做內容調整的不足[3]。現有AI預測相關研究多側重於演算法精準度的開發與優化，卻忽視了透過模型為學生提供即時、持續的學習反饋，難以直接落地提升學習品質，而這一缺口也成為當前AIEd領域的核心研究突破點[3]。針對此問題，相關研究將AI成績預測模型與學習分析方法深度整合，並在線上工程課程中開展準實驗驗證，結果證實此整合模式不僅能提升學生學習參與度、優化協作學習成績，更能有效增強整體學習滿意度，也為後續人工智能驅動學習分析的發展，提供了明確的範式啟示[3]。相較於基礎適應性學習的被動調整，此類進階模式更注重數據驅動的預判與反饋落地，真正落實以學習者為核心的個人化學習本質[1]。

整體而言，當前教育領域的學習型態已完成從「傳統單向灌輸教學」到「AI驅動多元學習生態」的關鍵典範轉移，歷經「系統主導、學習者被動接收」「被動響應、適性輔助」「預測驅動、即時反饋與個人化落地」三階段演進，各階段均有對應研究支撐其理論與實踐價值[1][2][3]。此一轉移過程累積了海量可量化、可追溯的學習行為數據，也衍生出關鍵研究難題：如何從龐雜的AI教育相關特徵中，執行有效且具可解釋性的特徵選擇，成為當前教育數據分析與學習成效預測領域的核心挑戰，也是銜接前文AI預測模型與學習分析應用的重要研究議題[3]。