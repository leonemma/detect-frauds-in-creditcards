# CreditCard-Faud-Detection

## Contents
- [Overview](#Overview)
- [Data](#Data)
- [Findings](#Findings)
 -[Statistical Analysis](#Statistical-Analysis) 
- [Machine Learning](#Machine-Learning)
- [Summary](#Summary)

## Overview
This notebook focuses on applying different machine learning algorithms to detect fraudulent transactions in credit card data. Fraud detection is a critical issue in the financial sector, where timely identification of fraudulent activities can prevent significant losses for both customers and businesses.  
We explored three different machine learning methods:
- Logistic regression
- Random forests
- Decision trees
The goal is to compare the performance of these methods in predicting whether a credit card transaction is fraudulent or not. By analyzing historical transaction data labeled with fraud indicators, we aim to build robust models capable of accurately identifying fraudulent activities.
## Data 
The dataset is available on Kaggle (Machine Learning Group - ULB · Andrea: [Creditcard Fraud Detection](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud))

The dataset contains transactions made by credit cards in September 2013 by European cardholders.
This dataset presents transactions that occurred in two days, where we have 492 frauds out of 284,807 transactions. The dataset is highly unbalanced, the positive class (frauds) account for 0.172% of all transactions.

It contains only numerical input variables which are the result of a PCA transformation. Unfortunately, due to confidentiality issues, we cannot provide the original features and more background information about the data. Features V1, V2, … V28 are the principal components obtained with PCA, the only features which have not been transformed with PCA are 'Time' and 'Amount'. Feature 'Time' contains the seconds elapsed between each transaction and the first transaction in the dataset. The feature 'Amount' is the transaction Amount, this feature can be used for example-dependant cost-sensitive learning. Feature 'Class' is the response variable and it takes value 1 in case of fraud and 0 otherwise.  

## Findings
- The dataset comprises 284,807 transactions recorded over a span of two days.
- The total amount of transactions is above $60,000
- In summary, due to credit card fraud, the bank incurred losses exceeding $60,000 over a span of two days
- The mean transaction amount for a fraud transaction is 122.21 and the for a non-fraud transaction is 88.29 . However, the largest fraud transaction amount is 2165.87$, unlike with a non-fraud transaction that is 25691.16 . We observe from the above boxplot that all transactions amount that are above 5000 are non-fraud.
  
### Statistical Analysis

## Machine Learning

## Summary
