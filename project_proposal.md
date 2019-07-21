<<<<<<< HEAD
### Lending Club Loan Repayment Analysis

**Business Overview**: Lending Club enables borrowers to create
unsecured personal loans between \$1,000 and \$40,000. The standard loan
period is three years. Investors can search and browse the loan listings
on Lending Club website and select loans that they want to invest in
based on the information supplied about the borrower, **amount of loan,
loan grade, and loan purpose**. Investors make money from interest.
Lending Club makes money by charging borrowers an origination fee and
investors a service fee.

**Problem Statement** -- how to predict the likelihood of a loan being
repaid in full, based on information supplied by the borrowers.

**Clients** - Investors who invest in the unsecured personal loans. The
analysis will help them to understand the risks of the unsecured loans
and identify loans that will more likely to be fully paid off. It will
also help investors to set higher interest rates for loans which may
have higher chances on default to compensate for the risks.

**Data Source** -- Lending Club provided historical loan information on
its [website](https://www.lendingclub.com/info/download-data.action).
The analysis will use 2007-2011 as training/testing data, and use
2012-2013 data to access error of the best model.

**Approach**

-   Data wrangling -- handling missing values, transforming data type,
    identify information can/cannot be used for model development

-   Exploratory -- observe loan paid off rate across time and individual
    features to identify obvious correlations

-   Inference Statistics -- among features observed in exploratory
    analysis, run chi-square test to confirm feature's significant on
    impacting loan paid off rates

-   Machine Learn -- this is a classification problem. Apply Logistic
    Regression and Random Forest model

**Deliverables**

-   Dedicated repository on GitHub that whole all related analysis for
    this project

-   Python codes that associated with data wrangling, exploratory,
    inference statistics, and machine learning

-   PowerPoint presentation for clients
