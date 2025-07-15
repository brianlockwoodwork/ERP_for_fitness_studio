# Google Sheets Business Toolkit

[This project](https://docs.google.com/spreadsheets/d/1WQeCAfbRjIPxgSVgwQHFGvEazNcwzVSTiosd9x9fu4Q/edit?usp=sharing) is a comprehensive business toolkit built in Google Sheets. It is designed to support in managing and analyzing operations across three core areas: Marketing, Finance, and Payroll.

![dashboard](/assets/main_dashboard.gif)

## All the links

[👉🏻 P&L, Cashflow and dashboards](https://docs.google.com/spreadsheets/d/1WQeCAfbRjIPxgSVgwQHFGvEazNcwzVSTiosd9x9fu4Q/edit?gid=939981570#gid=939981570)

[👉🏻 Salary Widget for Sales](https://docs.google.com/spreadsheets/d/1uBI8FtLOFW1EB8KTrBrZ8nmXv9CKlfTnuGUjMiXMZxw/edit?gid=278982829#gid=278982829)

[👉🏻 Transaction Log](https://docs.google.com/spreadsheets/d/1c7hDcup_u0AhyK11zYkaLzEZFhTqEgNo5fVgM8VUo5M/edit?gid=593220343#gid=593220343)

[👉🏻 Marketing Funnels](https://docs.google.com/spreadsheets/d/18UbCYCmYHT0UhvSi8QXXYHwRIDvc2aSxA5sjXRmFEW4/edit?usp=sharing)

[👉🏻 Exports *(technical source for all the tables above)*](https://docs.google.com/spreadsheets/d/1RNFbm5Liwbc_MEqer1T12WhgvPUN8cYNNmecbcPuHgg/edit?gid=288172794#gid=288172794)

## Table of Contents

- [Project Structure](#project-structure)
- [The Project](#the-project)
- [Financial Analysis](#financial-analysis)
- [Implementation steps](#implementation-steps)
- [Step 1: Digitalize the Transactions Log](#step-1-digitalize-the-transactions-log)
- [Step 2: Data Integration](#step-2-data-integration)
- [Step 3: Cashflow Sheet](#step-3-cashflow-sheet)
- [Step 4: Profit & Loss Sheet](#step-4-profit--loss-sheet)
- [Step 5: Membership Income](#step-5-membership-income)
- [Step 6: Additional Income Sources](#step-6-additional-income-sources)
- [Step 7: P&L Expense Categories](#step-7-pl-expense-categories)
- [Conclusion](#conclusion)
- [Closing Thoughts](#closing-thoughts)

## Project Structure

The toolkit is divided into three main parts:

### 1. Marketing Funnels

[Here is the description](/marketing_funnel/README.MD)

Provides a structured way to analyze marketing channels.
It enables to:

- Evaluate the performance of different sources
- Identify underperforming campaigns
- Allocate budget more effectively

### 2. Financial Analysis

Includes income, expense, and profit monitoring.
Built to help:

- Track key financial metrics
- Understand business health
- Make informed financial decisions

### 3. KPI Widget

Because payroll math shouldn’t feel like rocket science for the employees:

- Calculate employee salaries and bonuses
- Show their **KPI performance** in real-time
- Clearly display what they need to do to level up their paycheck

---


# The Project

> This project is tailored for operational use by fitness studios, though the logic and structure are applicable to many service-based businesses. The toolkit replaces manual notebooks and fragmented tools with a structured, formula-driven system. It integrates ERP data, financial logs, and performance metrics into a unified Google Sheets environment.
> 
> [👉 Click to explore the sheet](https://docs.google.com/spreadsheets/d/1WQeCAfbRjIPxgSVgwQHFGvEazNcwzVSTiosd9x9fu4Q/edit?usp=sharing) (viewer access).

---

## Financial Analysis

The financial analysis component addresses common issues found in ERPs that lack robust financial reporting. It enables:

- Accurate tracking of cashflow
- Real-time generation of Profit & Loss statements
- Visibility into actual business profitability

Why does that matter?
> Just because the bank account has money in it doesn't mean it’s yours.  
> At best? Maybe a quarter of it is actually yours. Maybe. 😅

---

## Implementation Steps

We began by evaluating the data sources already available. The findings included:

1. Sales data from the ERP system, including membership details and pricing  
2. A physical notebook used for manually recording expenses  

While limited, this data provided a starting point. From there, we initiated the process of building a structured and automated system using Google Sheets.

## Step 1: Digitalize the Transactions Log

To improve accuracy and scalability, we replaced the manual expense notebook with a structured digital log.

**The Transaction Log** serves as a centralized place to record all business expenses in a consistent format.

[View the Transaction Log](https://docs.google.com/spreadsheets/d/1c7hDcup_u0AhyK11zYkaLzEZFhTqEgNo5fVgM8VUo5M/edit?usp=sharing)

![Transaction Log](/assets/Transaction%20Log.png)

This became the foundational data source for all subsequent financial analysis and reporting.

---

## Step 2: Data Integration

With the Transaction Log established, the next step was to connect it to the main reporting dashboard.

This was done using the `IMPORTRANGE` function in Google Sheets, which allows data to be imported from one spreadsheet to another:

```excel
=IMPORTRANGE("https://docs.google.com/spreadsheets/d/1c7hDcup_u0AhyK11zYkaLzEZFhTqEgNo5fVgM8VUo5M/edit?gid=593220343#gid=593220343","TRANSACTION_LOG_WHOLE")
```

## Step 3: Cashflow Sheet

With the data successfully integrated, the next step was to build a structured and dynamic Cashflow sheet.

This sheet transforms raw transactional records into a clear view of the company's financial activity over time.

![cashflow_overview](/assets/cashflow_overview.gif)

The core calculation uses the following formula:

```excel
=SUMIFS(I_TL_EXPENCE, I_TL_CATEGORY, $E25, I_TL_PAYMENT_DATE, F$3, I_TL_BRANCH, '❌ Configuration'!$A$2)
```

## Step 4: Profit & Loss Sheet

The next phase involved building the Profit & Loss (P&L) sheet to track operational performance in terms of income and expenses.

The ERP system used by the client provided data on:

1. Membership check-ins  
2. Missed workouts  
3. Expired memberships  

We consolidated this data into a dedicated sheet called `Exports`, which serves as the central repository for all membership-related activity. This structured export allows for automated income calculations based on client behavior and membership status.

[View the data table](https://docs.google.com/spreadsheets/d/1RNFbm5Liwbc_MEqer1T12WhgvPUN8cYNNmecbcPuHgg/edit?gid=288172794#gid=288172794)  
[View data samples](/data_samples/)

![integration_exports](/assets//integration_exports.gif)

## Step 5: Membership Income

Using the data from the `Integration` sheet, income from memberships was calculated and included in the Profit & Loss (P&L) sheet. The figures were grouped by membership name and transaction date to ensure accurate reporting and historical comparisons.

This calculation combines revenue from three key sources:

1. Membership check-ins  
2. Expired memberships with remaining balances  
3. Missed sessions with associated charges  

The combined formula used is:

```excel
=SUMIFS(I_E_CHECK_INS_AMOUNT,I_E_CHECK_INS_DATE,PNL_DATE,I_E_CHECK_INS_MEMBERSHIP_NAME_IN_TABLE,$E9, I_E_CHECK_INS_BRANCH,'❌ Configuration'!$A$2)+SUMIFS(I_E_EXPIRED_MONEY_REMAINS,I_E_EXPIRED_MEMBERSHIP,$E9,I_E_EXPIRED_DATE, PNL_DATE,I_E_EXPIRED_BRANCH_1,'❌ Configuration'!$A$2)+SUMIFS(I_E_MISSED_AMOUNT,I_E_MISSED_DATE,PNL_DATE,I_E_MISSED_BRANCH,'❌ Configuration'!$A$2,I_E_MISSED_NAME_AS_IN_TABLE,$E9)
```
> 💡 $E9 = Membership Name

![P&L_overview](/assets/P&L_overview.gif)

## Step 6: Additional Income Sources

In addition to membership revenue, clients also generate income by renting out gym space and collecting an interest of deposits. These income streams are tracked separately and sourced from the Transaction Log.

[View the Transaction Log](https://docs.google.com/spreadsheets/d/1c7hDcup_u0AhyK11zYkaLzEZFhTqEgNo5fVgM8VUo5M/edit?gid=593220343#gid=593220343)

To calculate this type of revenue, we used the following formula:

```excel
=IFERROR(SUMIFS(I_TL_DAILY_INCOME,I_TL_CATEGORY,$E6,I_TL_BRANCH,'❌ Configuration'!$A$2,I_TL_START_DATE,"<="&PNL_DATE,I_TL_END_DATE,">="&PNL_DATE),0)
```
> 📌 $E6 = Income Category (like “Renting out studios” or “% of Deposit”)

## Step 7: P&L Expense Categories

Not all expense types can be aggregated using a single formula due to structural and categorical differences in the data. To ensure accuracy and maintain clarity, expenses were grouped into specific categories and calculated independently. These categories include:

1. Salaries  
2. Advertising Budget  
3. Transaction Fees  
4. Depreciation of Assets  

Each category has its own logic and dedicated formula within the spreadsheet. All calculations are fully automated and integrated into the Profit & Loss structure.

For users interested in the detailed logic and implementation:

[View the full spreadsheet and formula logic](https://docs.google.com/spreadsheets/d/1WQeCAfbRjIPxgSVgwQHFGvEazNcwzVSTiosd9x9fu4Q/edit?gid=2127869173#gid=2127869173)

# Conclusion

This toolkit transforms scattered operational data into a unified system for financial and business performance tracking. It provides:

•	A structured transaction logging system

•	Real-time cashflow visibility

•	An automated, transparent P&L statement

•	Integrated marketing and payroll metrics