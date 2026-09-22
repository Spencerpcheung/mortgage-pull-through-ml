# mortgage-pull-through-ml
Predict Pull Through with Machine Learning


# Mortgage Pull-Through Prediction

This project explores whether machine learning can be used to predict mortgage pull-through at the individual loan level.

The goal is to estimate the probability that a locked mortgage will ultimately fund using information available at the time of lock. These predicted probabilities can then be aggregated to estimate expected funded volume and potentially support pipeline forecasting and hedge management.

## Project Objective

Build and evaluate machine learning models that classify locked mortgage loans as:

- `1 = Funded`
- `0 = Fallout`

The project will focus on generating meaningful funding probabilities rather than only binary predictions.

## Why This Matters

Mortgage lenders face uncertainty between the time a loan is locked and the time it ultimately funds.

More accurate pull-through estimates may improve:

- expected funded volume forecasting
- pipeline exposure estimates
- hedge coverage decisions
- secondary market planning

## Machine Learning Approach

The project will compare multiple classification models, including:

- Logistic Regression
- Decision Tree
- Random Forest
- AdaBoost
- Gradient Boosting
- XGBoost

Model performance will be evaluated using metrics such as:

- Precision
- Recall
- F1 Score
- Confusion Matrix
- ROC-AUC
- Precision-Recall AUC

Probability calibration will also be evaluated because the model output may be used to estimate expected funded balances.



Project Documentation
See [PROJECT_SCOPING.md](PROJECT_SCOPING.md) for the detailed project scope, assumptions, candidate features, evaluation strategy, and data leakage considerations.
Data
No confidential employer or customer data will be published in this repository.
Any publicly shared version of the project will use public, anonymized, or synthetic mortgage data.

## Repository Structure

```text
mortgage-pull-through-ml/
│
├── README.md
├── PROJECT_SCOPING.md
├── data/
├── notebooks/
├── src/
└── results/