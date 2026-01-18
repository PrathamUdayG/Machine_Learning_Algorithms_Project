Telco Customer Churn Prediction using Random Forest
 Overview

This project builds a machine learning model to predict customer churn in a telecom company using a Random Forest classifier.

The objective is to identify customers who are likely to churn so that proactive retention strategies can be applied.
The focus is on a correct end-to-end machine learning workflow, not just maximizing accuracy.

 Dataset

Name: Telco Customer Churn Dataset (IBM)

Source: Kaggle

Rows: 7,043

Features: 21 (before encoding)

Target Variable: Churn

 Data Preprocessing
Target Variable

The Churn column contained mixed values (Yes/No, True/False)

Cleaned and converted to binary:

1 → Churn

0 → No Churn

Missing Values

No explicit null values initially

TotalCharges was stored as object due to blank strings

Converted to numeric using pd.to_numeric

Missing values (customers with zero tenure) were filled with 0

Feature Encoding

Binary categorical features → Label Encoding

Multi-category features → One-Hot Encoding

Identifier column (customerID) was dropped

Scaling

Not applied (tree-based models do not require feature scaling)

 Class Imbalance Handling

Churn rate ≈ 26.5%

Handled using class_weight='balanced'

Model evaluation prioritized:

Recall

F1 Score

ROC-AUC

Accuracy was not used as the primary metric

 Modeling Approach
Baseline Model

Random Forest classifier with class weighting

Used to establish baseline performance

Hyperparameter Tuning

GridSearchCV with 5-fold cross-validation

Scoring metric: ROC-AUC

Best Hyperparameters
n_estimators     : 400
max_depth        : 10
min_samples_leaf : 5
max_features     : log2
class_weight     : balanced

 Model Evaluation

Accuracy was not prioritized due to class imbalance.

Metrics Used

ROC-AUC

Recall

Precision

F1 Score

Performance Comparison
Model	ROC-AUC	Recall	Precision	F1 Score
Baseline RF	0.82	0.48	0.62	0.54
Tuned RF	0.85	0.77	0.54	0.63
Interpretation

ROC-AUC improvement indicates better class separation

Recall increased significantly, capturing more churn customers

Precision decreased slightly, which is acceptable for churn prediction use cases

 Feature Importance

Top contributing features:

TotalCharges

tenure

MonthlyCharges

Contract

PaymentMethod

InternetService

These features align well with real-world customer behavior.

Technologies Used

Python

Pandas

NumPy

Scikit-learn

Matplotlib

Conclusion:
This project demonstrates a practical and production-oriented machine learning pipeline for churn prediction.
The tuned Random Forest model achieves strong recall and ROC-AUC, making it suitable for real-world churn identification and retention strategies.

This project demonstrates a practical and production-oriented machine learning pipeline for churn prediction.

The tuned Random Forest model achieves strong recall and ROC-AUC, making it suitable for real-world churn identification and retention strategies.
