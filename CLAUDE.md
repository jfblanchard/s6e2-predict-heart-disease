# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Kaggle Playground Series Season 6, Episode 2 — binary classification to predict heart disease (Presence/Absence).

- Competition: https://www.kaggle.com/competitions/playground-series-s6e2
- Data: https://www.kaggle.com/competitions/playground-series-s6e2/data

## Environment

Python data science stack: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `scikit-learn`.

Run notebooks locally with Jupyter or upload to Kaggle. Data paths on Kaggle are `/kaggle/input/playground-series-s6e2/{train,test,sample_submission}.csv`.

```bash
jupyter notebook s6e2-predicting-heart-disease-eda.ipynb
```

## Dataset

- Train: 630,000 rows × 15 columns (including target)
- Test: 270,000 rows × 14 columns

**Target**: `heart_disease` — `"Absence"` / `"Presence"` (cast to 0/1 int8 for modeling)

**Categorical features**: `sex`, `chest_pain_type`, `fbs_over_120`, `ekg_results`, `exercise_angina`, `slope_of_st`, `number_of_vessels_fluro`, `thallium`

**Numeric features**: `age`, `bp`, `cholesterol`, `max_hr`, `st_depression`

## Conventions

- Column names are snake_cased (lowercase, spaces → underscores) via `clean_column_names()` defined in the notebook.
- Feature dtype casting is handled by `cast_features()`: binary columns → `int8`, ordinal categoricals → `category`, continuous → `float`.
- EDA helper `explore_feature_vs_target()` dispatches to numeric (boxplot + KDE + point-biserial corr) or categorical (positive rate + countplot) visualizations automatically based on dtype.

## Docs

Session logs go in `docs/` (create if needed).