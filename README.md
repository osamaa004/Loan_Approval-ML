# 🏦 Loan Eligibility Prediction Using Machine Learning

## Project Overview

This project aims to automate the loan approval process by predicting whether a loan application should be approved (`Loan_Status = Y`) or rejected (`Loan_Status = N`). Multiple machine learning algorithms were developed, optimized, and compared to identify the most reliable model for real-world deployment.

The complete workflow includes data preprocessing, feature engineering, hyperparameter tuning, model evaluation, and performance comparison using several classification metrics.

---

# Dataset Description

The project uses the **Loan Prediction Dataset**, containing **614 loan applications** and **13 features** describing applicant demographics, financial status, and credit information.

| Feature           | Description                      |
| ----------------- | -------------------------------- |
| Gender            | Applicant gender                 |
| Married           | Marital status                   |
| Dependents        | Number of dependents             |
| Education         | Education level                  |
| Self_Employed     | Employment type                  |
| ApplicantIncome   | Applicant monthly income         |
| CoapplicantIncome | Co-applicant monthly income      |
| LoanAmount        | Requested loan amount            |
| Loan_Amount_Term  | Loan repayment period            |
| Credit_History    | Previous credit repayment record |
| Property_Area     | Urban / Semiurban / Rural        |
| Loan_Status       | Target variable                  |

---

# Data Preprocessing & Feature Engineering

### Feature Engineering

A new feature called **TotalIncome** was created:

TotalIncome = ApplicantIncome + CoapplicantIncome

This feature better represents the total financial strength of the applicant's household compared to using the two income variables separately.

### Missing Value Handling

Missing values were imputed using:

* Mean Imputation for continuous numerical features.
* Mode Imputation for categorical and discrete features.

### Encoding

Different encoding strategies were used depending on feature type:

#### Ordinal Encoding

Applied to binary categorical variables:

* Gender
* Married
* Education

#### One-Hot Encoding

Applied to nominal variables:

* Property_Area
* Dependents
* Self_Employed

### Feature Scaling

Numerical features were standardized using:

* StandardScaler

This ensured proper convergence for algorithms sensitive to feature magnitude such as Logistic Regression and SVM.

### Outlier Analysis

A significant income outlier (~81,000) was detected.

Instead of removing it, the sample was retained because it represented an important edge case:

* High income
* Loan rejected

Keeping this observation helped models learn more realistic approval patterns rather than relying solely on income magnitude.

---

# Machine Learning Pipeline

A Scikit-Learn Pipeline combined with ColumnTransformer was implemented to ensure:

* Consistent preprocessing
* Prevention of data leakage
* Reproducible experiments

The dataset was divided into:

* Training Set: 70%
* Test Set: 30%

---

# Models Evaluated

## Logistic Regression

Used as the baseline linear classifier.

Experiments included:

* Standard Logistic Regression
* L1 Regularization (Lasso)
* L2 Regularization (Ridge)
* Hyperparameter-Tuned Logistic Regression

Best Accuracy:

**78%**

---

## Decision Tree

A non-linear model capable of learning hierarchical decision rules.

Experiments:

* Gini Criterion
* Entropy Criterion
* Hyperparameter-Tuned Tree

Best Accuracy:

**76%**

---

## Random Forest

An ensemble learning method that combines multiple decision trees through bagging to reduce variance and improve stability.

Experiments:

* Base Random Forest
* Hyperparameter-Tuned Random Forest

Best Accuracy:

**80%**

---

## AdaBoost

A boosting algorithm that iteratively focuses on previously misclassified samples.

Experiments:

* Base AdaBoost
* Hyperparameter-Tuned AdaBoost

Best Accuracy:

**79%**

---

## Support Vector Machine (SVM)

A powerful classifier capable of finding optimal separating boundaries in high-dimensional feature spaces.

Experiments:

* Base SVM
* Hyperparameter-Tuned SVM

Best Accuracy:

**79%**

---

# Hyperparameter Optimization

GridSearchCV with 5-Fold Cross Validation was used to optimize model parameters.

Examples:

### Logistic Regression

* C
* Penalty Type (L1 / L2)

### Decision Tree

* max_depth
* min_samples_split

### Random Forest

* n_estimators
* max_depth
* min_samples_split

### AdaBoost

* n_estimators
* learning_rate

### SVM

* C
* gamma
* kernel

---

# Model Performance Summary

| Model                       | Accuracy |
| --------------------------- | -------- |
| Logistic Regression (Base)  | 78%      |
| Logistic Regression (L1)    | 78%      |
| Logistic Regression (L2)    | 78%      |
| Logistic Regression (Tuned) | 78%      |
| Decision Tree (Gini)        | 74%      |
| Decision Tree (Entropy)     | 75%      |
| Decision Tree (Tuned)       | 76%      |
| Random Forest (Base)        | 78%      |
| Random Forest (Tuned)       | 80%      |
| AdaBoost (Base)             | 79%      |
| AdaBoost (Tuned)            | 78%      |
| SVM (Base)                  | 79%      |
| SVM (Tuned)                 | 78%      |

---

# Detailed Evaluation Metrics

| Model               | Accuracy | Precision | Recall | F1-Score | AUC  |
| ------------------- | -------- | --------- | ------ | -------- | ---- |
| Random Forest       | 80.0%    | 0.77      | 0.98   | 0.86     | 0.79 |
| Logistic Regression | 78.4%    | 0.76      | 0.98   | 0.86     | 0.70 |
| Decision Tree       | 78.4%    | 0.76      | 0.98   | 0.86     | 0.71 |
| AdaBoost            | 78.4%    | 0.76      | 0.98   | 0.86     | 0.72 |

---

# Results & Discussion

### Random Forest Performance

Random Forest achieved:

* Highest Accuracy (80%)
* Highest AUC (0.79)
* Strong Recall (98%)

The ensemble structure allowed the model to capture non-linear relationships while remaining robust against noise and outliers.

### Importance of Credit History

Results suggest that **Credit_History** is the most influential feature driving loan approval decisions. Simpler models were able to achieve competitive performance because this feature contains a strong predictive signal.

### False Positive Consideration

Although Random Forest achieved the highest overall performance, AdaBoost produced fewer False Positives in some experiments.

This can be advantageous in financial applications where approving an ineligible applicant carries significant risk.

Therefore:

* Random Forest is preferred for overall predictive performance.
* AdaBoost may be preferred when minimizing False Positives is the primary business objective.

---

# Conclusion

This project successfully developed and compared multiple machine learning models for loan approval prediction.

### Recommended Model

**Random Forest**

Reasons:

* Highest overall accuracy
* Best AUC score
* Robust to noise and outliers
* Strong generalization ability

### Business Insight

If the objective is maximizing approval detection while maintaining strong ranking capability, Random Forest is the best choice.

If minimizing risky approvals (False Positives) is the highest priority, AdaBoost becomes an attractive alternative despite its slightly lower overall accuracy.

The final system demonstrates how machine learning can support financial institutions by providing faster, more consistent, and data-driven loan approval decisions.
