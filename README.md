# Lending Club Loan Repayment Analysis


Lending Club enables borrowers to create unsecured personal loans between $1,000 and $40,000. The standard loan period is three years. Investors can search and browse the loan listings on Lending Club website and select loans that they want to invest in based on the information supplied about the borrower, **amount of loan, loan grade, and loan purpose**. Investors make money from interest. Lending Club makes money by charging borrowers an origination fee and investors a service fee.

**Objective:** 
- Predict the likelihood of loan repayment from an applicant based on applicant information

**Clients & Impact:** 
- Clients are the investors who invest in the unsecured personal loans The analysis will help investors understanding the risks of the unsecured loans and help them identify loans that will more likely be fully paid off. It will also help investors to set interest rates based on risks level.

**Data Source:** [Lending Club Statistics](https://www.lendingclub.com/info/download-data.action). 2007-2011 [Data Dictionary](https://github.com/sittingman/lending_repayment/blob/master/data_dict.ipynb)

**Approach:**

[**1.Data Wrangling**](https://github.com/sittingman/lending_repayment/blob/master/data_wrangling.ipynb)

The dataset has 144 features, in which 'loan_status' will serve as the target feature. 

Some columns have mostly missing data and will be dropped. Some information cannot be known in advance (e.g. late fees charged) so they cannot be used to develop the model. 

Some features will require data type modifications such as converting text into numeric values for model fitting later. 

The cleaned data has been saved off as a separate file to simplify data access.

[**2.Exploratory Analysis**](https://github.com/sittingman/lending_repayment/blob/master/data_exploratory.ipynb)

In the exploratory analysis part, we want to identify correlations (either positive or negative) among features with "loan paid off" rate through visualizations. The goal is to quickly identify high correlation variable before applying any machine learning algorithms.
Note: Loan paid off rate is calculated by all loans being paid off (target = 1) versus all loans (target = 1 + target = 0) within specific feature being observed. Target = 0 means loan defaulted.

**Findings**:  features that show potential correlations with the loan paid off rate are homeownership status, loan purpose, years of credit, Debt to Income ratio, % of credit usage, applicant's state. Data between 2007-2008 cannot be used as paid off rates were skewed by the financial crisis.

[**3.Inference Statistics**](https://github.com/sittingman/lending_repayment/blob/master/inference_stat.ipynb)

Post the exploratory analysis, we identified a few features that may correlate with the loan paid off rates. We now run statistical tests (chi-square) to ensure that the observed correlations are statistically significant.

**Findings**: All features selected indicate dependence to loan paid off rate and they can be used for machine learning. Debt to Income ratio (DTI) requires binning to show statistical dependence.

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


This problem is a classification problem. We will apply two methods and measure their accuracies (using F1 score) - Logistics Regression and Random Forest

We will use 2012-2013 loan data as final validation set to access the model prediction power ([test data transformation steps](https://github.com/sittingman/lending_repayment/blob/master/test_data_cleansing.ipynb))



