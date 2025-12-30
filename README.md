Loan Default Risk Prediction

End-to-end data reconciliation and machine learning pipeline for predicting loan default risk using real-world financial data.

Business Context

Financial institutions face challenges in accurately assessing credit risk due to fragmented data sources and inconsistent customer records.

This project focuses on building a loan-level default prediction system with strong emphasis on data reconciliation, feature integrity, and production-aligned modeling practices.

Problem Statement

Predict whether a loan will default using customer demographics, loan attributes, and historical repayment behavior.

Objectives:

Preserve loan-level granularity

Reconcile multiple inconsistent datasets

Prevent data leakage

Produce a modeling-ready dataset suitable for deployment

Datasets

Loan Application Data

4,368 loans

One row per loan

Contains target label

Customer Banking Profile

4,334 customer records

Demographic and banking attributes

Repayment History

18,183 historical loans

Used to derive behavioral features

Modeling Grain

One row represents one loan

This ensures:

Correct label alignment

No duplicate loans

Realistic credit risk modeling

Data Reconciliation Summary

Loan application table is used as the master dataset

Customer profiles are left-joined using customerid

Repayment history is aggregated per customer and merged as backward-looking features

No labeled loans are dropped

Coverage:

Total loans: 4,368

Loans with customer profiles: 3,269 (74.8 percent)

Loans with repayment history: 4,359 (99.8 percent)

Loans missing both profile and history: 4

Final Modeling Dataset

Shape: 4,368 rows by 20 features

Target distribution:

Good loans: 2,556

Bad loans: 713

Missing data handling:

Rows are preserved

Missing categorical values retained as explicit categories

Missing numeric values imputed

Missingness treated as informative

Feature Engineering Status

Feature engineering is performed after all data is aligned to the loan level.

Planned feature groups:

Demographic features

Financial features

Behavioral aggregates

Temporal features

Missingness indicators

Repository Structure

loan-default-risk

data

raw

interim

processed

notebooks

data_cleaning

data_reconciliation

feature_engineering

modeling

src

data

features

models

utils

reports

docker

tests

requirements.txt

README.md

.gitignore

Project Status

Data cleaning completed

Data reconciliation completed

Modeling dataset finalized

Feature engineering in progress

Modeling and deployment pending

Design Philosophy

This project prioritizes data correctness, transparency, and real-world applicability over shortcut modeling gains.

The goal is to build a production-ready loan default risk system.