# Predicting Serum Estradiol Concentrations with Machine Learning

An exploratory Python project using public **NHANES 2021–2023** data to investigate associations between estradiol and demographic, anthropometric and reproductive hormone measurements.

## Research question

How accurately can serum estradiol (pg/mL) be predicted from eight demographic and biological variables?

## Methods

The notebook merges NHANES hormone, demographic and body-measurement datasets by participant ID, explores distributions and associations, and compares a median baseline, Ridge Regression, Random Forest and histogram-based Gradient Boosting. Modelling uses complete observations with estradiol at or above the assay detection limit (5,131 participants); 4,104 are used for training and 1,027 for an exploratory test split. Models predict `log1p(estradiol)` and predictions are converted back to pg/mL for original-scale evaluation.

Predictors: sex, age, BMI, FSH, LH, progesterone, testosterone and sex hormone-binding globulin (SHBG).

## Selected findings

| Metric | Random Forest |
|---|---:|
| Five-fold training CV R² (log scale) | 0.788 |
| Five-fold training CV MAE (log scale) | 0.377 |
| Exploratory test R² (log scale) | 0.741 |
| Exploratory test R² (original scale) | 0.899 |
| Exploratory test MAE (pg/mL) | 17.24 |
| Test R² for actual estradiol <200 pg/mL | 0.677 |
| Test MAE for actual estradiol <200 pg/mL | 10.39 |

Gradient Boosting achieved mean cross-validated R² of 0.790 and MAE of 0.379 (log scale). The algorithms performed similarly; Random Forest was retained for its marginally lower CV MAE.

The original-scale R² was sensitive to very high estradiol values. All 20 highest measured concentrations belonged to participants recorded as pregnant, but pregnancy information was missing or inapplicable for many participants. Pregnancy subgroup findings are exploratory.

## Reproduce the analysis

1. Download `estradiol_prediction_clean.ipynb` or open it in Google Colab.
2. Install the packages listed in `requirements.txt` if necessary.
3. Run cells from top to bottom with internet access. The notebook downloads public NHANES XPT datasets from CDC servers.

## Limitations

The analysis does not account for NHANES survey design, uses complete cases, excludes below-detection target values, and has no independent external validation. The test set was inspected repeatedly during exploratory work and is not an untouched final holdout. Feature importance does not imply causality. This is a learning and research portfolio project, **not a clinical diagnostic model**.

## Data source

[CDC NHANES 2021–2023](https://wwwn.cdc.gov/nchs/nhanes/continuousnhanes/default.aspx?Cycle=2021-2023)
