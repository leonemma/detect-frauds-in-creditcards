# Credit Card Fraud Detection
- The source code for this project is available [here](https://github.com/leonemma/detect-frauds-in-creditcards/blob/main/creditcard-fraud-detector.ipynb)
## Contents
- [Overview](#Overview)
- [Data](#Data)
- [Findings](#Findings)
- [Machine Learning](#Machine-Learning)
   - [Considerations](#Considerations)
   - [Strategy](#Strategy)
   - [Model Evaluation](#Model-Evaluation)
   - [Model Comparison](#Model-Comparison)
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

The dataset contains transactions made by credit cards in September 2013 by European cardholders and presents transactions that occurred in two days, where we have 492 frauds out of 284,807 transactions.   
Additionally, the dataset is highly imbalanced since the positive class (frauds) accounts for 0.172% of all transactions and it contains only numerical input variables which are the result of a PCA transformation. Unfortunately, due to confidentiality issues, we cannot have access to the original features and more background information about the data. Features V1, V2, … V28 are the principal components obtained with PCA and the only features which have not been transformed with PCA are 'Time' and 'Amount'. 
- The feature 'Time' contains the seconds elapsed between each transaction and the first transaction in the dataset
- The feature 'Amount' is the transaction amount 
- The feature 'Class' is the response variable and it takes value 1 in case of fraud and 0 otherwise  

## Findings
- The dataset includes 284,807 transactions recorded over a span of two days
- The total amount of transactions is above $60,000
- In summary, due to credit card fraud, the bank incurred losses exceeding $60,000 over a span of two days
- The mean transaction amount for a fraud transaction is 122.21 and the for a non-fraud transaction is 88.29 . However, the largest fraud transaction amount is 2,165.87$, unlike with a non-fraud transaction that is 25,691.16$. We run the respective statistical t-test to ensure that the difference is statistically significant.

## Machine Learning
### Considerations
**Downsizing Majority Class for Computational Efficiency**  
- Dataset Reduction: The dataset reduction involved selecting a subset of 10,000 examples from the majority class randomly. This downsizing was performed to avoid the computational cost while ensuring a manageable dataset size for training.
- Selective Removal from Majority Class: Examples were removed exclusively from the majority class, which typically represents the negative class (non-fraudulent transactions) in the dataset.
  
**Impact on Model Performance**
- It's important to acknowledge that downsizing the majority class may lead to some loss of information from this class. Consequently, there might be implications for the model's ability to accurately detect instances of non-fraudulent transactions.

### Strategy
By using the validation set approach (train-test-split), some of the instances from the positive class will end up in the test set. Since the number of positive examples are significantly small, building a predictive model by using this method will lead to a significant loss of information for the positive class.
To avoid that, we are going to use the Cross Validation.  
- Stratified cross validation ensures that the proportion of the classes will be the same in every fold of K-fold CV.

### Model Evaluation
- Since the dataset is extremely inbalanced we will not focus on the accuracy metric. The accuracy tends to be misleading in extremely imbalanced datasets. In datasets like this, we expect accuracy be close to 0.99 . We care more about how the model performs in the positive class (fraud cases). Some metrics that we can use are the **recall score**, precision and **AUC-ROC curve**.
- Recall is a critical metric for detecting frauds in credit cards because it shows off the ability of the model to identify as many fraudulent transactions as possible.

     $$ Recall = \frac{True Positives}{True Positives+False Negatives} $$  

- The ROC curve is a graphical representation of the trade-off between true positive rate (recall/sensitivity) and false positive rate (1 - specificity) at various threshold settings for the model.
- The AUC (Area Under the Curve) is a metric used to evaluate the performance of a binary classification model.
   - Range: AUC values range from 0 to 1, where:
   - AUC = 1 indicates a perfect classifier that achieves perfect separation between the positive and negative classes.
   - AUC = 0.5 indicates a classifier that performs no better than random guessing.  

For this reason, **Recall and AUC-ROC Curve will be the metrics that we will use on the model evaluation.**

### Models Optimization
After training the initial models — Decision Trees, Random Forests, and Logistic Regression, we focused on optimizing their performance for fraud detection.
Given that in fraud detection recall (the ability to identify actual frauds) is more critical than precision, we optimized each model by adjusting the decision threshold rather than relying on the default 0.5.

- By trying different values for threshold using K-Fold Cross Validation, each model achieved a significant improvement in recall score, successfully identifying more fraudulent transactions.
- This optimization introduced a trade-off as well. Although recall increased, precision decreased slightly, meaning more false positives were accepted in exchange for catching more real frauds which is a necessary compromise in high-risk domains like fraud detection.
  
### Model Comparison
The ROC Curves below indicate that the Random Forest has the best performance across different threshold values and discriminates better the two classes comparing to Logistic Regression and Decision Trees classifiers.
This is confirmed by the AUC (Area Under the Curve) value which is the highest for Random Forests (0.95).      

![ROC_Curves](https://github.com/leonemma/detect-frauds-in-creditcards/blob/main/plots/AUC.png)    

From the barplot below, it's obvious that Random Forests achieved the highest recall score among the three models.   

![Recall_Scores](https://github.com/leonemma/detect-frauds-in-creditcards/blob/main/plots/Recall_Scores_bars.png)    

|       Model         | Recall | AUC  | 
|---------------------|--------|------|
| Logistic Regression | 0.868  | 0.95 |
|    Random Forests   | 0.892  | 0.97 |
|    Decision Trees   | 0.864  | 0.91 |

## Summary
Random Forests had the best performance in correctly identifying positive instances compared to Logistic Regression and Decision Trees and is chosen as the main model for detecting a fraud transaction.
In summary, the machine learning model identifies successfully almost the 90% of fraudulent transactions, resulting in savings of $54,000 within a two-day period and over 2.4 million over three months.
