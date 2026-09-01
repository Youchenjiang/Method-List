# Positive/Negative Text Polarity Classification Report

## 1. Task Overview

This assignment is based on the in-class Kaggle competition **Positive/Negative: Text Polarity Classification 26**. The goal is to classify each text sample into one of two labels:

| Label | Meaning |
|---:|---|
| `0` | negative |
| `1` | positive |

The evaluation metric is classification accuracy on the hidden Kaggle test labels. The main challenge is not the output format itself, but the ambiguity of sentiment polarity. Some texts contain mixed sentiment, indirect tone, or polarity that depends on the final clause. The training set is also much smaller than the test set, so validation stability and overfitting control are important.

The expected submission format is a CSV file with exactly two columns:

```text
row_id,LABEL
```

All final submissions were checked for row count, binary labels, and `row_id` alignment against `dataset/test_no_answer_2022.csv`.

## 2. Reproducibility Setup

The implementation was written in Python. The main packages were:

- `pandas` and `numpy` for data processing
- `scikit-learn` for sparse baselines and logistic stacking
- `torch` and `transformers` for Transformer fine-tuning
- `huggingface_hub` for loading pretrained checkpoints

The main hardware used for Transformer training was an NVIDIA GeForce RTX 4060 Laptop GPU.

The final reproducibility workflow is documented in:

```text
docs/reproducibility_workflow.md
```

The project also includes a validator:

```bash
python scripts/utils/validate_reproduction_artifacts.py
```

This script checks that the final OOF probability files, test probability files, and selected submission files exist and are aligned. The final validation output was:

```text
Reproduction artifact validation passed.
Train rows: 2000
Test rows: 11000
OOF branches: 3
Test probability branches: 3
Final submissions: 2
```

The main reproducibility controls were:

1. fixed random seeds, mainly seed `42`
2. stratified 5-fold validation
3. saved out-of-fold probabilities for training data
4. saved averaged test probabilities for each model branch
5. strict `row_id` alignment before all ensemble operations

## 3. Overall Experimental Workflow

The project was organized as a staged workflow. Each stage had a specific purpose, and the result of one stage determined the next step. The goal was not to randomly try many models, but to build a reproducible path from a simple baseline to a stronger final ensemble.

```text
Dataset check
  -> sparse TF-IDF baselines
  -> first Transformer anchor (RoBERTa)
  -> K-fold probability artifact pipeline
  -> second backbone test (DeBERTa-base)
  -> two-model fusion diagnosis
  -> sentiment-specialized third backbone
  -> formal 5-fold third-model fine-tuning
  -> three-model OOF stacking and soft-vote
  -> final Kaggle submission selection
```

The full workflow can be summarized as follows:

| Stage | Main Question | Action | Decision Produced |
|---|---|---|---|
| Sparse baseline | Can simple text features solve the task? | Train TF-IDF linear models | Baseline was stable but too weak |
| Single Transformer | Does contextual representation help? | Fine-tune RoBERTa | RoBERTa became the first strong anchor |
| K-fold artifacts | How can later ensembles avoid leakage? | Save OOF and test probabilities | Standard artifact format for all later branches |
| Second backbone | Does another architecture add complementary signal? | Train DeBERTa-base and combine with RoBERTa | Two-model fusion improved only slightly |
| Third backbone | What information is still missing? | Test sentiment-specialized Elron model | Sentiment prior looked useful but needed fine-tuning |
| Formal third model | Can the third model be made comparable to other branches? | Fine-tune Elron with the same 5-fold protocol | Third branch became the strongest local model |
| Final ensemble | How should the three branches be combined? | Compare OOF stacking and soft-vote | Stacking was best; soft-vote was a strong hedge |

This flow is the central experimental logic of the project. The later result tables should be read as evidence for these decisions, not as isolated score records.

## 4. Baseline Experiments

I first built sparse text baselines to establish a reproducible lower bound. The baseline approach used TF-IDF features with linear classifiers. Both word n-grams and character n-grams were tested because the input text is semi-processed and may contain short fragments, punctuation, and irregular spacing.

The main baseline results were:

| Experiment | Main Idea | Local OOF Accuracy |
|---|---|---:|
| Initial TF-IDF Logistic Regression | word + character TF-IDF | `0.6825` |
| Best sparse/context baseline | controlled n-gram and normalization tests | `0.6875` |

These results showed that sparse features could provide a stable lower bound, but they were not sufficient for ambiguous polarity classification. Their role was therefore not to be the final method, but to establish a reproducible reference point before using more expensive Transformer models. This motivated the move to contextual representations.

## 5. Transformer K-fold Pipeline

The first strong Transformer model was `roberta-base`. The strongest early RoBERTa configuration was named R04:

| Setting | Value |
|---|---|
| model | `roberta-base` |
| learning rate | `2e-5` |
| epochs | `3` |
| max length | `128` |
| weight decay | `0.01` |
| label smoothing | `0.0` |

The early RoBERTa anchor submission was:

| Candidate | Public Score | Private Score |
|---|---:|---:|
| `candidate_01_R04.csv` | `0.75647` | `0.76648` |

After this, I moved to stratified K-fold probability artifacts. Each model branch produced:

1. OOF probabilities for the training rows
2. averaged test probabilities across folds
3. a Kaggle submission candidate
4. a markdown experiment report

This artifact design made later soft-voting and stacking possible without training the meta-model on in-sample predictions.

This became the main engineering standard of the project:

| Artifact Type | Purpose |
|---|---|
| OOF probability file | Train or evaluate ensemble logic on training rows without in-sample base predictions |
| Test probability file | Generate final test predictions after row alignment |
| Submission CSV | Upload to Kaggle |
| Markdown report | Record settings, metrics, and output paths |

The key idea is that every serious model branch had to be converted into the same probability format. This made later comparisons and ensemble generation reproducible.

## 6. Two-model Fusion

The second Transformer branch was `microsoft/deberta-base`. The reason for adding it was to test whether a different Transformer architecture could provide complementary errors rather than simply repeating RoBERTa.

The DeBERTa-base 5-fold branch produced:

| Model | OOF Accuracy | OOF F1 |
|---|---:|---:|
| DeBERTa-base | `0.8160` | `0.8180` |

Several RoBERTa + DeBERTa fusion methods were tested:

| Candidate | Method | Public Score | Private Score |
|---|---|---:|---:|
| `candidate_day3_roberta_seed42_plus_deberta_base_seed42_softvote.csv` | equal-weight soft-vote | `0.75399` | `0.76716` |
| `candidate_day3_roberta70_deberta30_softvote.csv` | weighted soft-vote 0.7/0.3 | `0.75399` | `0.76852` |
| `candidate_day3_roberta80_deberta20_softvote.csv` | weighted soft-vote 0.8/0.2 | `0.75151` | `0.76770` |
| `candidate_day4_upside_roberta_deberta_oof_stacking_v1.csv` | OOF logistic stacking | `0.75564` | `0.76824` |

The two-model results showed limited improvement. DeBERTa added some complementary signal, but the two-model ensemble still did not create a clear breakthrough over the original RoBERTa anchor.

This was an important turning point in the workflow. If a second general-purpose Transformer backbone only produced small gains, then the next step should not be another similar generic model. The next model needed to add a different kind of information. Because the task was explicitly sentiment polarity classification, I looked for a sentiment-specialized backbone.

## 7. Third-model Formalization

After the two-model fusion plateau, I introduced `Elron/deberta-v3-large-sentiment` as a third model. This was not a random larger model. It was chosen because it is sentiment-specialized and could provide polarity-related knowledge that general RoBERTa and DeBERTa checkpoints may lack.

I first tested the checkpoint as a zero-shot sentiment model. This exploratory probe showed useful sentiment signal, but it was not strong enough to use directly as the final branch:

| Exploratory Probe | Value |
|---|---:|
| zero-shot Elron train proxy accuracy | `0.7750` |
| zero-shot Elron train proxy F1 | `0.7372` |
| zero-shot Elron train proxy logloss | `0.5758` |
| zero-shot test label counts | `{0: 7368, 1: 3632}` |
| early three-model ArchB stacking OOF accuracy | `0.8375` |
| early three-model ArchB stacking OOF F1 | `0.8361` |

Therefore, I formalized the third branch by fine-tuning it with the same stratified 5-fold protocol as the other Transformer branches. The implementation also repaired incompatible Hugging Face `id2label` metadata when needed and rebuilt the model as a two-class classifier.

The formal fine-tuned Elron branch produced:

| Model | OOF Accuracy | OOF F1 | OOF LogLoss |
|---|---:|---:|---:|
| fine-tuned Elron DeBERTa-v3-large sentiment | `0.8635` | `0.8634` | `0.5918` |

This was the first major route-level improvement and justified using the third model in the final ensemble.

## 8. Final Reproduction Procedure

The final submission can be reproduced from three model branches and two ensemble scripts. The final branch artifacts were:

| Branch | OOF Artifact | Test Probability Artifact |
|---|---|---|
| RoBERTa R04 | `reports/artifacts/roberta_kfold_oof_seed42_r04_fix.csv` | `reports/artifacts/test_prob_seed42_r04_fix.csv` |
| DeBERTa-base | `reports/artifacts/deberta_base_kfold_oof_seed42.csv` | `reports/artifacts/test_prob_deberta_base_seed42.csv` |
| Elron sentiment model | `reports/artifacts/elron_deberta_v3_large_sent_kfold_oof_seed42.csv` | `reports/artifacts/test_prob_elron_deberta_v3_large_sent_kfold_seed42.csv` |

The best final stacking submission was generated with:

```bash
python scripts/ensemble/train_stacking_meta.py \
  --oof reports/artifacts/roberta_kfold_oof_seed42_r04_fix.csv reports/artifacts/deberta_base_kfold_oof_seed42.csv reports/artifacts/elron_deberta_v3_large_sent_kfold_oof_seed42.csv \
  --test reports/artifacts/test_prob_seed42_r04_fix.csv reports/artifacts/test_prob_deberta_base_seed42.csv reports/artifacts/test_prob_elron_deberta_v3_large_sent_kfold_seed42.csv \
  --meta-c 1.0 \
  --output submission_candidates/submitted_frozen/candidate_day5_formal_3way_stacking_elron_kfold.csv
```

The final soft-vote hedge was generated with:

```bash
python scripts/ensemble/generate_softvote_ensemble.py \
  --inputs reports/artifacts/test_prob_seed42_r04_fix.csv reports/artifacts/test_prob_deberta_base_seed42.csv reports/artifacts/test_prob_elron_deberta_v3_large_sent_kfold_seed42.csv \
  --weights 0.05 0.45 0.50 \
  --output submission_candidates/submitted_frozen/candidate_final_softvote_r05_d45_e50_oofopt.csv
```

After generation, I validated the files with:

```bash
python scripts/utils/validate_reproduction_artifacts.py
```

This procedure is the most important part of reproduction. A reader does not need to rerun every exploratory experiment to reproduce the final submission logic; they need the dataset, the scripts, the three branch probability artifacts, and the final ensemble commands.

## 9. Ensemble Methods

Two ensemble strategies were used for the final model pool.

### 9.1 Soft-vote

Soft-vote combines model probabilities with fixed weights. If the three model probabilities are `p_roberta`, `p_deberta`, and `p_elron`, the final positive probability is:

```text
p_positive =
  w_roberta * p_roberta
+ w_deberta * p_deberta
+ w_elron * p_elron
```

The final optimized soft-vote used weights:

| Model | Weight |
|---|---:|
| RoBERTa R04 | `0.05` |
| DeBERTa-base | `0.45` |
| Elron DeBERTa-v3-large sentiment | `0.50` |

### 9.2 OOF Logistic Stacking

Stacking uses each model's OOF positive-class probability as a feature:

```text
X = [
  roberta_oof_prob_1,
  deberta_oof_prob_1,
  elron_oof_prob_1
]
y = LABEL
```

A Logistic Regression meta-model was trained on OOF probabilities only. It was then applied to the aligned test probability files. This avoids direct in-sample leakage because the meta-model never trains on base-model predictions generated from the same examples used to fit those base models.

## 10. Final Results

The main public and private leaderboard results were:

| Candidate | Method | Public Score | Private Score |
|---|---|---:|---:|
| `candidate_01_R04.csv` | RoBERTa single-model anchor | `0.75647` | `0.76648` |
| `candidate_day4_upside_roberta_deberta_oof_stacking_v1.csv` | RoBERTa + DeBERTa stacking | `0.75564` | `0.76824` |
| `candidate_day5_formal_softvote_r50_d20_e30.csv` | three-model conservative soft-vote | `0.77548` | `0.78819` |
| `candidate_day5_formal_3way_stacking_elron_kfold.csv` | three-model OOF stacking | `0.78925` | `0.79796` |
| `candidate_final_3way_stacking_c03_elron_kfold.csv` | regularized three-model stacking | `0.78815` | `0.79728` |
| `candidate_final_softvote_r05_d45_e50_oofopt.csv` | OOF-optimized three-model soft-vote | `0.78760` | `0.79769` |

The final selected submissions were:

| Role | File | Public Score | Private Score | Reason |
|---|---|---:|---:|---|
| Primary | `candidate_day5_formal_3way_stacking_elron_kfold.csv` | `0.78925` | `0.79796` | best public and private score |
| Hedge | `candidate_final_softvote_r05_d45_e50_oofopt.csv` | `0.78760` | `0.79769` | method-diverse hedge |

The final Kaggle score was:

```text
0.79796
```

The displayed final rank was:

```text
20
```

## 11. Decision Logic and Discussion

The largest improvement came from adding and fine-tuning the sentiment-specialized third model. The two-model RoBERTa + DeBERTa experiments showed that cross-backbone diversity helped, but the improvement was small. The Elron branch changed the model pool more substantially because it introduced a sentiment-specific prior.

The final comparison also showed why selecting two highly similar stacking submissions was not ideal. The regularized C=0.3 stacking variant had a private score of `0.79728`, while the optimized soft-vote hedge had a private score of `0.79769`. Although the soft-vote hedge was slightly lower than the best stacking model, it used a different fusion rule and was very close on the private leaderboard. This supports the final strategy of selecting one best stacking submission and one method-diverse hedge.

An important engineering lesson was that probability alignment matters. An earlier incorrect ensemble that mixed probability artifacts improperly scored around random performance. Later scripts therefore enforced strict `row_id` alignment and required probability columns before generating ensemble submissions.

The final decision logic was:

| Decision | Reason |
|---|---|
| Use Transformer models after sparse baselines | Sparse features were stable but too weak for ambiguous sentiment |
| Use K-fold artifacts | Single split validation was not reliable enough, and ensembles required leakage-safe OOF probabilities |
| Add DeBERTa-base | A second architecture could test cross-backbone complementarity |
| Move beyond two generic backbones | Two-model fusion plateaued near the original RoBERTa anchor |
| Add Elron sentiment model | The missing signal was likely sentiment-specific rather than just architectural diversity |
| Fine-tune Elron instead of using zero-shot output | The zero-shot probe showed signal but not enough direct accuracy |
| Select stacking as primary | It had the best public and private score |
| Select optimized soft-vote as hedge | It used a different fusion rule and nearly matched stacking on private score |

This is why the final result should be understood as a controlled progression from simple reproducible baselines to a task-specialized three-model ensemble, rather than a collection of unrelated submissions.

## 12. Conclusion

This project followed a staged experimental procedure rather than a single large model trial. Sparse TF-IDF baselines established a lower bound, RoBERTa provided the first strong Transformer anchor, DeBERTa tested cross-backbone complementarity, and the sentiment-specialized Elron model provided the decisive third branch after formal 5-fold fine-tuning.

The best final submission was the three-model OOF logistic stacking candidate:

```text
candidate_day5_formal_3way_stacking_elron_kfold.csv
```

It achieved:

```text
Public score:  0.78925
Private score: 0.79796
```

The main conclusion is that the final performance gain came primarily from formalizing the task-specialized third backbone, while OOF stacking provided the strongest final use of the expanded model pool.
