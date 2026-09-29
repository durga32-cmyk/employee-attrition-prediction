# Employee Attrition Prediction

Predicts which employees are likely to leave a company, using the IBM HR Analytics dataset (1,470 employees, 35 original features).

## Dataset

IBM HR Analytics Employee Attrition dataset, loaded directly from a public CSV URL in the notebook (no manual download needed — just run the notebook top to bottom).

## Pipeline

- Data cleaned and encoded (categorical → numeric via one-hot encoding)
- Stored in a PostgreSQL database (Neon) and queried back via SQL
- Split into train/test sets (80/20, stratified)
- Features scaled for Logistic Regression

## Models compared

| Model | Accuracy | Precision (leavers) | Recall (leavers) | F1 (leavers) |
|---|---|---|---|---|
| Logistic Regression | 0.861 | 0.615 | 0.340 | 0.438 |
| Random Forest (balanced) | 0.840 | 0.500 | 0.085 | 0.145 |
| Naive Bayes | 0.721 | 0.312 | 0.617 | 0.414 |

Since only ~16% of employees in the dataset actually left, plain accuracy is misleading — models are compared primarily on **recall and F1 for the "leaves" class**, since catching at-risk employees matters more than overall accuracy.

## Key findings from EDA

- Employees working overtime leave at roughly 3x the rate of those who don't
- Lower job satisfaction and lower income both correlate with higher attrition
- Correlation alone is weak for any single feature — no one factor predicts attrition on its own

## Tech used

Python, pandas, scikit-learn, SQLAlchemy, PostgreSQL (Neon)
