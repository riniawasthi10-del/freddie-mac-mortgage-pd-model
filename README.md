# Freddie Mac Mortgage PD Model

An applied **probability-of-default (PD)** modeling pipeline built on Freddie Mac single-family loan-level data. The project combines SQL-based feature engineering with predictive modeling, probability calibration, and out-of-time validation.

## Research question

Can loan-level origination information be transformed into a useful 36-month probability-of-default model, and does that model generalize to a later mortgage vintage?

## Pipeline

1. **Data ingestion** — parse origination and performance files and construct a correctly seasoned 36-month default target.
2. **SQL feature engineering** — load the analytical data into SQLite and use joins, aggregations, and window functions.
3. **Modeling** — compare Logistic Regression and XGBoost using scikit-learn pipelines for imputation and categorical encoding.
4. **Calibration** — evaluate predicted probabilities using calibration curves and isotonic calibration.
5. **Validation** — compare in-sample performance with a 2022 out-of-time cohort.

## Results

- In-sample ROC-AUC: **0.8118**
- In-sample KS: **0.4869**
- 2022 OOT ROC-AUC: **0.683**
- The OOT evaluation shows a meaningful calibration break and performance deterioration, highlighting the importance of temporal validation under changing interest-rate conditions.

The performance drop is treated as a finding, not hidden: a credit model that ranks borrowers well in one period can degrade when the underlying economic regime changes.

## Key skills

**SQL · SQLite · Python · scikit-learn · XGBoost · probability calibration · credit-risk validation · temporal/OOT evaluation**

## Notebooks

1. `00_data_ingestion.ipynb` — source parsing, default-target construction, data cleaning, and preprocessing
2. `01_sql_database_and_features.ipynb` — SQL database construction, feature engineering, modeling, calibration, and OOT evaluation

Raw Freddie Mac source files are not included in this repository.

## Data availability

The repository does not include the underlying loan-level source files or generated SQLite database. Obtain the permitted Freddie Mac sample/source files separately and place them under `./data/` before running the notebooks.
