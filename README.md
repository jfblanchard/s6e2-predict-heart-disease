# S6E2 — Predict Heart Disease

Kaggle Playground Series Season 6, Episode 2. Binary classification to predict heart disease (Presence/Absence). Evaluated on AUC.

- Competition: https://www.kaggle.com/competitions/playground-series-s6e2
- Data: https://www.kaggle.com/competitions/playground-series-s6e2/data

## Result

**~550 / ~4000 (top 13%)** | Best LB: **0.95382**

## What Worked

- **CatBoost (CPU, float64)** — consistently the best model throughout. Default depth 6 was already optimal; tuning rarely helped.
- **Divye FE** — the only genuine gain: frequency encoding + OOF target encoding + C(8,2)=28 pairwise interaction products. Gave +0.00022 CV / +0.00024 LB.
- **Cross-cat pairs as cat_features** — C(6,2)=15 categorical pair combinations passed directly to CatBoost as additional categorical features. Marginal +0.00001 LB on top of Divye FE.

## What Didn't Work

- GBT tuning (depth, l2, rsm, bagging) — at most +0.00004 CV, within noise
- Seed averaging — flat to slightly negative at 630k rows; single model already at minimum variance
- Stacking and ensembling — base models too correlated (>0.999) to gain diversity
- Neural nets (TabNet, FT-Transformer, TabM, RealMLP) — all ~0.002 AUC below CatBoost; synthetic tabular data is GBT-optimal
- Extended feature engineering (3-way interactions, groupby stats, joint target encoding) — flat or negative
- Pseudo-labeling, external UCI data, monotone constraints — no gain or actively hurt

## Takeaways for Next Competition

- On Playground Series synthetic data, prioritize strong public FE kernels over tuning or ensembling
- CatBoost CPU float64 is the reliable baseline; establish it early
- Stacking/ensembling is only worth exploring if base model correlation is below ~0.998
- Adversarial validation early rules out distribution shift strategies quickly
- CV-to-LB gap was ~0.002 and very stable — useful for calibrating which CV deltas are worth a submission slot