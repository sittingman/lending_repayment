# Lending Club Loan Repayment Analysis


Lending Club enables borrowers to create unsecured personal loans between $1,000 and $40,000. The standard loan period is three years. Investors can search and browse the loan listings on Lending Club website and select loans that they want to invest in based on the information supplied about the borrower, amount of loan, loan grade, and loan purpose. Investors make money from interest. Lending Club makes money by charging borrowers an origination fee and investors a service fee.

**Objective:** 
- Predict the likelihood of paid off for loans that were approved by Lending Club. 

**Clients & Impact:** 
- Clients are the investors who invest in the unsecured personal loans and Lending Club credit risks team. The analysis aims to help them to identify approved loans that may have high risks of default based on historical information. Lending Club can put more attention to monitor those loans in order to plan contingencies on risk mitigation.

**Data Source:** [Lending Club Statistics](https://www.lendingclub.com/info/download-data.action). 2007-2013 [Data Dictionary](https://github.com/sittingman/lending_repayment/blob/master/data_dict.ipynb)
- Use data from 2007-2012 as train set, and 2013 data as final test data

**Approach:**


**Note**: To run all the notebooks on personal station, please first download "data" zip file, extract and put the files into a folder called "data" right next to all the jupyter notebooks.

[**1.Data Wrangling**](https://github.com/sittingman/lending_repayment/blob/master/data_wrangling.ipynb)

The dataset has 144 features, in which 'loan_status' will serve as the target feature.

Some columns have mostly missing data and will be dropped. Some information cannot be known in advance (e.g. settlement date) and cannot be used to develop the model.

Some features will require data type modifications such as converting text into numeric values for model training.

The cleaned data has been saved off as a separate file to simplify data access.



[**2.Exploratory Analysis**](https://github.com/sittingman/lending_repayment/blob/master/data_exploratory.ipynb)

In the exploratory analysis part, we want to identify correlations (either positive or negative) among features with "loan paid off" rate through visualizations. The goal is to quickly identify high correlation variables before applying any machine learning algorithms. Note: Loan paid off rate is calculated by all loans being paid off (target = 1) versus all loans (target = 1 + target = 0) within specific feature being observed. Target = 0 means loan defaulted.

**Findings**: features that show potential correlations with the loan paid off rate are homeownership status, loan purpose, years of credit, Debt to Income ratio, % of credit usage, applicant's state. Data between 2007-2008 cannot be used as paid off rates were skewed by the financial crisis.

[**3.Inference Statistics**](https://github.com/sittingman/lending_repayment/blob/master/inference_stat.ipynb)

Post the exploratory analysis, we identified a few features that may correlate with the loan paid off rates. We now run statistical tests (chi-square) to ensure that the observed correlations are statistically significant.

**Findings**: All features selected indicate dependence to loan paid off rate and they can be used for machine learning.

[**4. Machine Learning**](https://github.com/sittingman/lending_repayment/blob/master/machine_learning.ipynb)

We have identified the useful features that could help to predict whether the loan will be paid off or default.
Here is the summary

| Target | Features |
| ------ | -------- |
|loan_status| purpose |
|           | homeownership|
|           | credit history |
|           | Debt to Income Ratio (DTI)|
|           | Number of credit line |
|           | Applicant State |


This problem is a classification problem. We will apply two methods and measure their accuracies (using F1 score and Ty) - Logistics Regression and Random Forest

For the first phrase modeling, we will focus on the numeric variables, which are 
- years of credit
- DTI
- total credit lines

The remaining variables will be accessed in the next phrase for model improvement.

**Findings**

Below is the performance summary among baseline (no modeling), Logistic Regression, and Random Forest

|Model | F1 score (cross validated)| Type 1 error | Type 2 error |
|----- | -------|------|-------|
|Baseline | 0.9154| 3,431 (15%) | 0 (0%) |
|Logistic Regression | 0.6704 | 1,616 (7.2%) | 8585 (38%) |
|Random Forest | 0.9203 | 3,077 (13.7%) | 1584 (7%) |

Logistic Regression has the smallest Type 1 error, which makes it a winner for the analysis. On the flip side, it introduces significant Type 2 error, which may result in unnecessary efforts on monitoring misclassified high risks loans. Lending Club could prioritize efforts based on the loan amount. As a next step, we will add loan amount as a new feature to identify any correlations among loan amount and paid off rate.

### Conclusion

- Lending Club has its own set of credit underwriting policy. Loan requests that didn't meet the policy were declined. Approved loans had an average of ~15%-18% of default rate, which is higher than residential and consumer loans default rates within the United States during periods based on [FRB](https://www.federalreserve.gov/releases/chargeoff/delallsa.htm)
- Applying Logistic Regression algorithms as suggested by the above analysis will help Lending Club to identify ~9% of the high risks loans in advance. This enables Lending Club to monitor those loans and plan contingency to minimize loss should default happens. It helps Lending Club to lower its overall default rate as low as 6%, which is more in line with the industry standard.
- The model does introduce Type 2 error which may result in unnecessary efforts on monitoring misclassified high risks loans. Lending Club should prioritize efforts based on the loan amount. As a next step, we will add loan amount as a new feature to evaluate if loan amount may impact paid off rate to reduce Type 2 error.

### Further Improvements

- Introduce categorical features and also loan amount into the model to access if we can obtain further improvement on reducing Type 1 error.
- Cross-validation should be done in the form of Time Series Nested Cross-Validation to avoid contamination of time component on predicting results. For example, business cycles are time-sensitive and could impact the individuals' ability to pay off loans. The current validation methodology ignored the timing impacts.
- Access 1-2 more classification models to have a broader measurement for model performance. I would consider Extreme Gradient Boosting and Support Vector Machines, for example.
- Features engineering which includes clustering to capture potential patterns that were not captured by looking at one feature alone.
- Run correlation test across features to confirm that features are independent of each other



