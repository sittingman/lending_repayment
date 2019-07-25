# Lending Club Loan Repayment Analysis


Lending Club enables borrowers to create unsecured personal loans between $1,000 and $40,000. The standard loan period is three years. Investors can search and browse the loan listings on Lending Club website and select loans that they want to invest in based on the information supplied about the borrower, amount of loan, loan grade, and loan purpose. Investors make money from interest. Lending Club makes money by charging borrowers an origination fee and investors a service fee.

**Objective:** 
- Predict the likelihood of paid off for loans based on information provided by borrowers at the point of application. The model should be able to screen out high risk loan requests and not rejecting good loans request by mistake. The metric we use for evaluating models will be [F1 score](https://en.wikipedia.org/wiki/F1_score). In this study, target 0 = default, target 1 = paid off.


**Clients & Impact:** 
- Clients are the investors who invest in the unsecured personal loans and Lending Club credit risks team. The analysis aims to help them to identify loan requests that may have high default rate based on historical information. Hence, Lending Club can minimize loss on granting bad loans.

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

We have identified the features that could help predicting loan default/paid off.
Here is the summary:

| Target | Features |
| ------ | -------- |
|loan_status| purpose |
|           | homeownership|
|           | credit history |
|           | Debt to Income Ratio (DTI)|
|           | Number of credit line |
|           | Applicant State |


This is a classification problem. We will apply two methods and measure their accuracies (using F1 score) - Logistics Regression and Random Forest

For the first phrase modeling, we will focus on the numeric variables, which are 
- years of credit
- DTI
- total credit lines

The remaining variables will be accessed in the next phrase for model improvement.

**Findings**

Below is the performance summary among baseline (no modeling), Logistic Regression, and Random Forest

|Model | F1 score (cross validated)| misclassification rate |
|----- | -------|------|
|Baseline | 0.917| .15 |
|Logistic Regression | 0.670 | .46 |
|Random Forest | 0.883 | .21 |

Random Forest has more stable performance based on its high F1 score.

### Conclusion

1. Random Forest has balanced performance (high F1 score). 
2. The model enables Lending Club to filter out some bad loan requests which would reduce profit loss driven by loan defaults. However, the model introduces type 2 error which represents loss revenue by rejecting loan requests that would paid off. Lending Club would need to weigh between the two trade offs and define the threshold tolerance on the potential misclassification. 
2. From Data Exploratory Analysis, we identified that loan purpose is likely to impact loan paid off rate. A lot of applicants work in the military.

### Further Improvements

- Introduce categorical features into the model to seek further improvement on F1 score.
- Cross-validation should be done in the form of Time Series Nested Cross-Validation to avoid contamination of time component on predicting results.
- Access 1-2 more classification models to have a broader measurement for model performance. I would consider Extreme Gradient Boosting and Support Vector Machines, for example.
- Features engineering which includes clustering to capture potential patterns that were not captured by looking at one feature alone.
- Run correlation test across features to access potential collinearity.


[#### Presentation Slides](https://github.com/sittingman/lending_repayment/blob/master/Loan_repayment.pdf)
