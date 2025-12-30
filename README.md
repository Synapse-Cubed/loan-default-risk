# Loan Default Risk Prediction 


End-to-end data reconciliation and machine learning pipeline for predicting loan default risk.


## Business Context

Financial institutions face challenges in accurately assessing credit risk due to fragmented data sources and inconsistent customer records.

This project focuses on building a loan-level default prediction system with strong emphasis on data reconciliation, feature integrity, and production-aligned modeling practices.


## Problem Statement

Predict whether a loan will default using customer demographics, loan attributes, and historical repayment behavior.

### Objectives:

- Predict whether a loan will default
- Preserve loan-level granularity
- Prevent data leakage
- Align with real-world credit scoring workflows


## Datasets

- Loan application data containing 4,368 loans with target labels
- Customer banking profiles with demographic and account attributes
- Historical repayment records used to derive behavioral features


## Modeling Grain

- One row represents one loan
- All features are aligned to the loan level
- Historical data is strictly backward-looking


## Data Reconciliation Summary

- Loan application table is used as the master dataset
- Customer profiles are left-joined using customerid
- Repayment history is aggregated per customer before merging
- No labeled loans are dropped during reconciliation


## Coverage:

- Total loans: 4,368
- Loans with customer profiles: 3,269
- Loans with repayment history: 4,359
- Loans missing both profile and history: 4


## Final Modeling Dataset

- Dataset shape: 4,368 rows by 20 features
- Target variable: good_bad_flag
- Class distribution reflects real-world imbalance


## Missing Data Strategy

- Rows are preserved to avoid selection bias
- Missing categorical values are retained as explicit categories
- Missing numeric values are imputed
- Missingness is treated as potentially informative


## Feature Engineering Status

Feature engineering is performed after all data is aligned to the loan level.

- Demographic features
- Financial features
- Behavioral aggregates
- Temporal features
- Missingness indicators


## Project Status

- Data cleaning completed
- Data reconciliation completed
- Modeling dataset finalized
- Feature engineering in progress


## Repository Structure

loan-default-risk/
│
├── data/
│   ├── raw/
│   │   ├── loan_application.csv
│   │   ├── customer_banking_profile.csv
│   │   └── repayment_history.csv
│   │
│   ├── interim/
│   │   ├── loan_application_cleaned.csv
│   │   ├── customer_banking_profile_cleaned.csv
│   │   └── repayment_history_cleaned.csv
│   │
│   └── processed/
│       └── loan_level_model_dataset.csv
│
├── notebooks/
│   ├── 01_data_cleaning/
│   ├── 02_data_reconciliation/
│   ├── 03_feature_engineering/
│   └── 04_modeling/
│
├── src/
│   ├── data/
│   ├── features/
│   ├── models/
│   └── utils/
│
├── models/
│   ├── trained/
│   └── metrics/
│
├── reports/
│   ├── eda/
│   └── model_performance/
│
├── docker/
│   ├── Dockerfile
│   └── docker-compose.yml
│
├── tests/
│
├── requirements.txt
├── Makefile
└── README.md



## Design Philosophy

This project prioritizes data integrity, reproducibility, and real-world modeling practices over shortcut performance gains.

The goal is to build a production-aligned loan default risk system.
