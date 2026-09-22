# Mortgage Pull-Through Prediction

## Business Problem
We want to predict future mortgage pull-through using historical lock performance. The population will include all incoming locks regardless of their eventual status. By estimating how many locked loans are expected to fund versus fall out, we can better understand expected funded volume and overall pipeline performance. This is important to Secondary Marketing because expected pull-through directly affects how much pipeline exposure we expect to retain and how much hedge coverage may be needed. More accurate predicted values could therefore improve both forecasting and hedge management.

## Machine Learning Problem
This project will be treated as a supervised binary classification problem. The model will use historical mortgage lock data to predict whether an incoming locked loan is expected to ultimately fund or fall out of the pipeline.

The goal is to generate a funding probability for each lock rather than only a simple funded/not-funded prediction. These individual probabilities can then be aggregated to estimate expected future funded volume and support pull-through forecasting.

## Target Variable
The target variable will represent the final outcome of each locked loan.

- `1 = Funded`
- `0 = Fallout`

A loan may be classified as funded when a valid funding date is present.

A loan may be classified as fallout when the loan does not fund and has a terminal status such as withdrawn or denied. The action date may be used to determine when the fallout event was processed.

Additional status definitions may be required after reviewing the available data to ensure that canceled, expired, withdrawn, denied, and other terminal statuses are treated consistently.

## Prediction Point
The initial prediction point will be the time the loan is locked.

Only information available at or before the lock date should be used to generate the initial prediction.

This allows the model to answer:

> Based on what we know when the loan is locked, what is the probability that this loan will eventually fund?

Future versions of the model may explore updated predictions as the loan moves through the pipeline.

## Candidate Features
Candidate features may include borrower, loan, lock, pricing, and market characteristics.

### Borrower and Loan Characteristics
- FICO score
- DTI
- LTV
- CLTV
- loan amount
- loan purpose
- occupancy
- property type
- number of units
- first-time homebuyer indicator
- loan program
- channel

### Lock Characteristics
- lock date
- initial lock term
- expected closing date
- days from lock to expected closing
- loan amount at lock
- product type

### Pricing and Market Characteristics
- note rate
- prevailing mortgage rate
- spread between locked rate and market rate
- Treasury yield
- mortgage-backed securities market movement
- interest-rate movement around the lock date

### Time-Based Features
- month
- quarter
- day of week
- seasonality

Feature selection may change after exploratory data analysis and review of the available dataset.

## Candidate Models
The project will begin with a simple baseline and then compare multiple classification models.

Candidate models include:

- Logistic Regression
- Decision Tree
- Random Forest
- AdaBoost
- Gradient Boosting
- XGBoost

Logistic Regression will provide an interpretable baseline, while tree-based and boosting models may capture nonlinear relationships and interactions between variables.

## Evaluation Metrics
Accuracy alone will not be sufficient because the funded and fallout populations may not be evenly distributed.

The following metrics will be considered:

- Accuracy
- Precision
- Recall
- F1 Score
- Confusion Matrix
- ROC-AUC
- Precision-Recall AUC

Because the model may ultimately be used to estimate expected funded volume, probability calibration will also be important.

For example:

`Expected Funded Balance = Loan Amount × Predicted Funding Probability`
The model should therefore produce probabilities that are meaningful, not only correct classifications.

## Data Leakage Risks
Data leakage will be an important concern because some loan information may only become available after the initial lock.

Examples of possible leakage include:

- final funding date
- final loan status
- withdrawal or denial action date
- post-lock underwriting decisions
- closing confirmation
- later lock extensions
- final approval milestones

These fields may be used to create the target variable, but they should not be used as predictors for a model that is intended to make a prediction at the time of initial lock.

## Data Strategy
Historical lock-level data will be used to build the modeling dataset.

The dataset should include all incoming locks regardless of final status so that both funded and fallout outcomes are represented.

Historical records will be used to determine the final outcome of each lock using fields such as funding date, loan status, and action date.

For a public portfolio version of this project, confidential company or customer information should not be published. Public, anonymized, or synthetic data should be used for any externally shared version of the project.

## Success Criteria
The project will be considered successful if it can:

- build an end-to-end pull-through prediction workflow
- predict funded versus fallout outcomes better than a simple baseline
- produce useful loan-level funding probabilities
- identify factors associated with higher or lower pull-through
- compare multiple machine learning models
- avoid data leakage
- translate predicted probabilities into expected funded volume
- provide results that could support pull-through forecasting and hedge coverage analysis