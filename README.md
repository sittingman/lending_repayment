# Lending Club Loan Repayment Analysis


**Objective:** Predict likelihood of loan repayment from an applicant.

**Impact:** Minimize chance of granting loans to applicants who would have high chance of default, which translate to profit loss to the lender

**Clients:** Lending Club loans underwriters 

**Data Source:** [Lending Club Statistics](https://www.lendingclub.com/info/download-data.action/). 2007-2011 [Data Dictionary](https://github.com/sittingman/lending_repayment/blob/master/data_dict.ipynb)

**Approach:**

The dataset has 144 features, in which 'loan_status' will serve as the target feature. Then narrow down to features that have no or few missing values. Also disregard features that cannot be known in advance (e.g. late fees charged). Use visualization to assess the rest to identify ones that have either positive or negative correlation to the default rate. Apply classification models to find the best features set that has the highest prediction accuracy.

[**Data Wrangling**](https://github.com/sittingman/lending_repayment/blob/master/data_wrangling.ipynb)

[**Exploratory Analysis**](https://github.com/sittingman/lending_repayment/blob/master/data_exploratory.ipynb)
