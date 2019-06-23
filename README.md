# Lending Club Loan Repayment Analysis


LendingClub enables borrowers to create unsecured personal loans between $1,000 and $40,000. The standard loan period is three years. Investors can search and browse the loan listings on LendingClub website and select loans that they want to invest in based on the information supplied about the borrower, **amount of loan, loan grade, and loan purpose**. Investors make money from interest. LendingClub makes money by charging borrowers an origination fee and investors a service fee.

**Objective:** 
- Predict likelihood of loan repayment from an applicant based on applicant information

**Clients & Impact:** 
- Clients are the investors who utlimately invest on the unsecured personal loans The analysis will help investors on undestand the rishs of the unsecured and increase the chance of investing in loans that will be fully paid off. It will also help investors to set interest rates based on risks should they want to invest on higher risks loans.

**Data Source:** [Lending Club Statistics](https://www.lendingclub.com/info/download-data.action/). 2007-2011 [Data Dictionary](https://github.com/sittingman/lending_repayment/blob/master/data_dict.ipynb)

**Approach:**

The dataset has 144 features, in which 'loan_status' will serve as the target feature. Some of the columns have mostly missing data as those involve personal privacy and will dropped. Some information cannot be known in advance (e.g. late fees charged) so thely cannot be used to develop the model either. 

The steps of data cleasing can be found below:

[**Data Wrangling**](https://github.com/sittingman/lending_repayment/blob/master/data_wrangling.ipynb)

In the exploratory analysis part, we will try to identify correleation (either positive or negative) among features with loan "paid off" rates. Loan paid off rate is calculated by all loans being paid off (target = 1) versus all loans (target = 1 + target = 0) within specific feature being observed.

[**Exploratory Analysis**](https://github.com/sittingman/lending_repayment/blob/master/data_exploratory.ipynb)

Post the exploratory analysis, we identified few features that may have correleation with loan paid off rates. We now need to run statistical tests (chi-square) to ensure that the observed correlations are statistically significant.


[**Inference Statistics**](https://github.com/sittingman/lending_repayment/blob/master/inference_stat.ipynb)
