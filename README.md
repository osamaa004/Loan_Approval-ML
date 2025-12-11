## Dataset Description

| Column Name        | Meaning             | Explanation (Simple)                                           | Example                    |
|-------------------|-------------------|---------------------------------------------------------------|----------------------------|
| Loan_ID           | Loan Identifier    | Unique ID for each loan application                           | LP001002                   |
| Gender            | Applicant’s Gender | Whether the applicant is Male or Female                       | Male, Female               |
| Married           | Marital Status     | Whether the applicant is married or not                       | Yes, No                    |
| Dependents        | Number of Dependents | Number of people dependent on the applicant (kids, family)   | 0, 1, 2, 3+                |
| Education         | Education Level    | Applicant’s education background                              | Graduate, Not Graduate     |
| Self_Employed     | Employment Type    | Whether the applicant is self-employed or not                | Yes, No                    |
| ApplicantIncome   | Applicant’s Income | Monthly income of the main applicant                          | 5000                       |
| CoapplicantIncome | Co-applicant’s Income | Monthly income of co-applicant (e.g., spouse)               | 2000                       |
| LoanAmount        | Loan Amount        | Amount of loan applied (in thousands)                         | 128 = 128,000              |
| Loan_Amount_Term  | Loan Term          | Time period of the loan (in months)                           | 360 months = 30 years      |
| Credit_History    | Credit History     | Record of applicant’s past credit repayment (1 = good, 0 = bad)| 1, 0                      |
| Property_Area     | Property Location  | Area type where the property is located                       | Urban, Semiurban, Rural    |
| Loan_Status       | Target Variable    | Whether the loan was approved or not                          | Y = Approved, N = Not Approved |





## Model Performance Summary

| Model                     | Accuracy |
|---------------------------|----------|
| Logistic Regression (Base) | 78%      |
| Logistic Regression (L1)   | 78%      |
| Logistic Regression (L2)   | 78%      |
| Logistic Regression (Tuned)| 78%      |
| Decision Tree (Gini)       | 74%      |
| Decision Tree (Entropy)    | 75%      |
| Decision Tree (Tuned)      | 76%      |
| Random Forest (Base)       | 78%      |
| Random Forest (Tuned)      | 78%      |
| AdaBoost (Base)            | 79%      |
| AdaBoost (Tuned)           | 78%      |
| SVM (Base)                 | 79%      |
| SVM (Tuned)                | 78%      |

**Best Model (in my opinion):**  
Adam without grid search, because it gives the **lowest False Positives (FP = 34)**, which is my main concern.
