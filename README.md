# House Price Prediction using Linear Regression

## Overview
This project builds a baseline **house price prediction model** using **Linear Regression**.  
The focus is on understanding the **end-to-end machine learning workflow**, including data cleaning, preprocessing, feature engineering, and model evaluation.

Rather than using complex models, the goal was to create a **clean, interpretable, and well-structured regression pipeline**.

---

## Dataset
- **Name:** House Prices – Advanced Regression Techniques  
- **Source:** Kaggle  
- **Link:** https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques  
- **Rows:** 1460  
- **Columns:** 81 (including target)

**Target Variable**
- `SalePrice` — selling price of the house

---

## Tools & Libraries
- Python  
- NumPy  
- Pandas  
- Scikit-learn  

---

## Project Workflow

### 1. Data Loading & Cleaning
- Loaded dataset using Pandas
- Dropped the `Id` column

### 2. Missing Value Handling
- Numerical features filled with **median**
- Categorical features filled with **mode**
- Result: no missing values

### 3. Outlier Handling
- Applied **IQR-based clipping** for numerical features
- No rows were removed
- Special handling for `LotArea`:
  - 1st–99th percentile clipping
  - Log transformation to reduce skewness

### 4. Target Variable Transformation
- `SalePrice` was right-skewed
- Applied `log1p(SalePrice)` to:
  - Reduce skewness
  - Improve linear regression performance
  - Stabilize variance

### 5. Categorical Feature Handling
- Identified categorical columns using data types
- Dropped high-cardinality categorical features (>10 unique values)
- Kept feature space simple and interpretable for Linear Regression

### 6. Feature Encoding
- Applied **One-Hot Encoding**
- Used `drop='first'` to avoid dummy variable trap
- Handled unseen categories safely

### 7. Feature Scaling
- Scaled numerical features using **StandardScaler**
- Categorical dummy variables were not scaled

### 8. Train-Test Split
- 80% training, 20% testing split
- Used a fixed `random_state` for reproducibility

### 9. Model Training
- Trained a **Linear Regression** model on processed data

---

## Model Evaluation

### Metrics Used
- R² Score
- RMSE (Root Mean Squared Error) on log scale

### Results
| Metric | Train | Test |
|------|------|------|
| R² Score | 0.9375 | 0.8751 |
| RMSE (log) | 0.0976 | 0.1527 |

---

## Conclusion
- The model generalizes well on unseen data
- Slight train–test gap indicates mild overfitting
- Serves as a **strong baseline Linear Regression model**
- Can be extended using:
  - Ridge / Lasso Regression
  - Tree-based models

---

## Future Improvements
- Reintroduce high-cardinality categorical features using regularization
- Try Ridge and Lasso regression
- Compare with tree-based models (Random Forest, XGBoost)
