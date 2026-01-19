# Breast Cancer Diagnosis – Decision Tree & Random Forest (EDA + Modeling)

## Project Overview
This project focuses on performing **Exploratory Data Analysis (EDA)** and building **tree-based classification models** to predict whether a breast tumor is **malignant or benign** using the Breast Cancer Wisconsin (Diagnostic) dataset.

The primary goal is to understand how **Decision Trees and Random Forests** behave with respect to feature distributions, correlation, feature selection, and overfitting, rather than applying unnecessary preprocessing.

---

## Dataset Information

- **Dataset Name:** Breast Cancer Wisconsin (Diagnostic)
- **Source:** UCI Machine Learning Repository  
- **Dataset Link:**  
  https://archive.ics.uci.edu/ml/datasets/Breast+Cancer+Wisconsin+(Diagnostic)

- **Shape:** `(569, 31)`
- **Target Column:** `diagnosis`
  - `1` → Malignant  
  - `0` → Benign  

Each feature represents computed characteristics of cell nuclei obtained from digitized images of fine needle aspirate (FNA) biopsies.

---

## Data Cleaning & Preprocessing

The following steps were performed:

- Dropped the `id` column (non-informative identifier)
- Removed the column with only null values (`Unnamed: 32`)
- Encoded the target variable:
  - `M → 1`
  - `B → 0`
- No feature scaling or skewness correction was applied, as tree-based models are invariant to monotonic transformations

---

## Exploratory Data Analysis (EDA)

### 1. Target Class Distribution
- Benign (0): **357 samples**
- Malignant (1): **212 samples**

This represents a **mild class imbalance (~63% vs ~37%)**, which does not require resampling for tree-based models.

---

### 2. Feature Distribution by Class
- Boxplots were used to compare key features across benign and malignant classes
- Features such as `radius_mean`, `perimeter_mean`, `area_mean`, and `concavity_mean` showed clear separation
- This explains why tree-based models perform well on this dataset

---

### 3. Correlation Analysis
- Strong correlations were observed among groups of features (e.g., radius, perimeter, area)
- Correlated features were **not removed**, as:
  - Decision Trees select splits based on thresholds
  - Random Forests use feature bagging to reduce correlation impact

---

### 4. Skewness & Multicollinearity
- Skewness and multicollinearity were analyzed but **not corrected**
- These issues primarily affect linear models, not tree-based models
- Retaining correlated features helps Random Forests leverage feature diversity

---

## Feature Selection (RFE)

- **Recursive Feature Elimination (RFE)** was applied using a constrained Decision Tree
- Purpose: **feature relevance analysis**, not aggressive feature removal
- A subset of 10 important features was selected
- RFE was used only for analysis; all features were retained for Random Forest training

---

## Model Training & Evaluation

### Decision Tree
- Controlled using:
  - `max_depth`
  - `min_samples_split`
  - `min_samples_leaf`
  - `max_features`
- Training vs validation accuracy was analyzed across different tree depths to visualize overfitting

---

### RFE vs Full Feature Comparison (Decision Tree)

| Model | Training Accuracy | Validation Accuracy |
|-----|------------------|--------------------|
| Decision Tree (All Features) | 0.9516 | 0.9561 |
| Decision Tree (RFE Features) | 0.9626 | 0.9649 |

**Observation:**  
RFE slightly improved validation accuracy, indicating feature redundancy. However, the improvement is marginal, and all features were retained for ensemble models.

---

### Random Forest
- Used to reduce variance and improve generalization
- Performance evaluated using:
  - Accuracy
  - Precision
  - Recall
  - ROC-AUC score
- ROC curves were plotted to compare Decision Tree vs Random Forest performance

---

## Key Takeaways

- Tree-based models handle skewness and multicollinearity naturally
- Mild class imbalance does not require resampling
- Recursive Feature Elimination is useful for **analysis**, not mandatory feature removal
- Random Forests generalize better than single Decision Trees
- ROC-AUC and recall are more informative than accuracy alone for medical classification tasks

---

## Tools & Libraries
- Python
- pandas, numpy
- scikit-learn

---

## Conclusion
This project demonstrates a **methodical, model-aware EDA workflow** and highlights why Decision Trees and Random Forests are effective for structured medical datasets with correlated features.
