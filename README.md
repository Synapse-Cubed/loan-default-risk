Loan Default Risk Prediction

An End-to-End Machine Learning & MLOps Project

1. Business Problem

Financial institutions face persistent challenges in accurately assessing loan default risk, especially when customer behavior, financial capacity, and historical repayment patterns are fragmented across multiple data sources.

Traditional rule-based credit scoring methods often:

- Fail to capture complex borrower behavior

- Do not scale well with growing data

- Are slow to adapt to changing risk patterns

Objective:
Develop a robust, data-driven machine learning pipeline that predicts loan default risk at the loan level, enabling:

- Better credit approval decisions

- Reduced non-performing loans


- Improved portfolio risk management


2. Project Scope & Solution Overview

This project builds an end-to-end loan default risk prediction system, covering:

- Multi-table data cleaning & integration

- Leakage-safe feature engineering

- Supervised ML modeling

- Model packaging and deployment (MLOps)

The solution is designed to reflect real-world banking constraints, not just academic modeling.


3. Data Sources

The dataset consists of three relational tables, each representing a different aspect of borrower information.

3.1 Loan Application (loan_application)

Role: Label authority & modeling base table
Rows: 4,368
Grain: One row = one loan

Key columns:

- customerid

- systemloanid

- loannumber

- loanamount

- totaldue

- termdays

good_bad_flag (target variable)

This table defines the model universe.
Only loans present here are allowed in training or inference.


3.2 Customer Banking Profile (customer_banking_profile)

Role: Demographic, employment, and geospatial context
Rows: 4,334
Grain: One row = one customer

Key features:

- Age

- Employment status

- Bank account type

- Bank name

- Latitude / Longitude

- Engineered state feature (from coordinates)

- Missing values are retained intentionally and handled during feature engineering.

3.3 Repayment History (repayment_history)

Role: Historical loan behavior
Rows: 18,183
Grain: One row = one loan (historical)

Key features:

- Loan amounts and tenure

- Due and repayment dates

- Loan lifecycle timestamps

This table contains all historical loans, including those without labels.
It is filtered strictly to labeled loans before modeling.


4. Modeling Grain & Data Integrity

A critical design decision:

- One row in the final dataset represents one loan.

- Labels exist only at the loan level

- No transaction-level repayment events are assumed

- All joins are performed using:

customerid + systemloanid + loannumber


This prevents:

- Duplicate loan leakage

- Inflated performance metrics

- Unrealistic deployment assumptions


5. Data Leakage Prevention Strategy

To ensure production realism:

- The loan application table defines reality

- Repayment history is filtered using labeled loans only

- Customer data is left-joined (never used to filter loans)

- No future information is introduced into features

- This mirrors how credit risk models are deployed in practice.


6. Missing Data Philosophy

Missing values are treated as informative signals, not errors.

Key principles:

- No row is dropped (labels are expensive)

- Missing categorical values → "Unknown"

- Missing numeric behavioral features → domain-aware imputation

- Missingness indicators are engineered where relevant

- This approach aligns with real credit-scoring systems, where absence of history can itself indicate risk.


7. Feature Engineering (Ongoing)

- Planned feature categories include:

- Demographic features: age, employment status, location

- Financial features: loan amount, tenure, total due

- Behavioral proxies: historical loan patterns

- Temporal features: durations between loan events

- Missingness indicators

- Feature engineering is performed after all tables are aligned to the loan level.


8. Repository Structure
loan-default-risk/
│
├── data/
│   ├── raw/                # Original datasets
│   ├── interim/            # Cleaned individual tables
│   └── processed/          # Final model-ready dataset
│
├── notebooks/
│   ├── 01_data_cleaning/
│   ├── 02_feature_engineering/
│   └── 03_modeling/
│
├── src/
│   ├── data/               # Reproducible data pipelines
│   ├── features/           # Feature engineering logic
│   ├── models/             # Training & evaluation code
│   └── utils/
│
├── models/                 # Saved model artifacts
├── reports/                # EDA and evaluation outputs
│
├── docker/                 # Docker & container configs
├── .gitignore
├── requirements.txt
├── README.md
└── Makefile


9. MLOps & Deployment Roadmap

The project is designed to evolve into a production-ready system, including:

Reproducible training pipelines

- Model versioning

- Dockerized inference service

- Scalable deployment (API-based)

- Clear separation between training and inference logic


10. Current Status

- Data cleaning completed (all tables)

- Correct loan-level alignment achieved

- Leakage-safe joins implemented

- Feature engineering in progress

- Model training & evaluation pending

- Deployment & containerization upcoming


11. Key Design Principle

This project prioritizes correctness, realism, and business alignment over quick accuracy gains.

The goal is not just to build a model —
but to build a credible credit risk system.