# Bank-Loan-Dashboard

### Dashboard Link : [https://app.powerbi.com/groups/me/reports/a0926578-c9ee-40f7-9e1b-68aa872e48bf/19f5da4b545ec08b6000?experience=power-bi]

## Problem Statement

Bank loans are a crucial financial tool that enables individuals and businesses to achieve their goals and manage financial needs. Banks collect and analyse loan data — from loan applications, credit reports, internal transaction records, online portals and third-party sources — to assess risk, support lending decisions, manage loan portfolios, detect fraud, stay compliant with regulations, and understand customer behaviour.

This project analyses a bank's loan portfolio to give the bank's management a clear, data-driven view of its lending business. The dashboard is built in two stages — first using **MS SQL Server** to store the data and answer business questions through SQL queries, and then using **Power BI** to turn those answers into an interactive, visual report — so that results from SQL, Power BI and Excel can be compared against one another.

The same business questions and KPIs — Total Applications, Total Funded Amount, Total Amount Received, Average Interest Rate, Average DTI, Good Loan vs Bad Loan split, and regional/segment-wise trends (state, term, purpose, employment length, home ownership) — were reproduced using pandas for data analysis and matplotlib/seaborn for visualization, to compare how the same insights come out across different tools.

The dashboard is designed to help the bank:

- Track the overall volume and health of loan applications (Total Applications, Total Funded Amount, Total Amount Received), including Month-to-Date (MTD) figures and Month-over-Month (MoM) change, so trends can be spotted early.
- Monitor the average Interest Rate and average Debt-to-Income Ratio (DTI) across the portfolio, since these directly reflect the cost of lending and the borrowers' financial health.
- Separate loans into **Good Loans** (Fully Paid / Current) and **Bad Loans** (Charged Off) so that the bank can immediately see what portion of its lending is performing well versus what portion is at risk.
- Break down loan performance by **Loan Status** in a grid view, so underperforming categories of loans can be identified quickly.
- Understand *where* and *from whom* the lending demand is coming from — by region (state), loan term, purpose, employment length and home ownership — so marketing and risk strategies can be tailored to the right customer segments.
- Give analysts and relationship managers a **Details view** where they can drill into individual loan records for day-to-day operational use.

In short, because the bank cannot manage what it cannot see, this dashboard turns raw loan data into a single source of truth the bank can use to reduce risk, improve decision-making, and grow its loan book responsibly.

### Steps followed

- **Step 1 :** Loan data was imported into **MS SQL Server** and a dedicated database was created to hold it.
- **Step 2 :** A table was created in SQL Server and the raw loan data was loaded into it.
- **Step 3 :** SQL queries were written to explore the data and answer the underlying business questions — using `SELECT`, `GROUP BY`, `ORDER BY`, `COUNT`, `DISTINCT`, `CAST`, `DECIMAL`, date functions such as `DATENAME`, `DATEPART`, `MONTH`, `QUARTER`, `DAY`, `HOUR`, as well as window functions like `CTE` and `PARTITION BY`.
- **Step 4 :** The same queries and results were cross-checked against **Power BI** and **Excel** to make sure the numbers matched regardless of the tool used, since the underlying data and logic remain the same.
- **Step 5 :** Power BI Desktop was connected directly to the MS SQL Server database as the data source.
- **Step 6 :** In Power Query, the data was cleaned and shaped — checking column quality, distribution and profile (based on the entire dataset, not just the default 1000-row preview), fixing data types, and handling blank/erroneous values before loading it into the data model.
- **Step 7 :** Data modelling was carried out in Power BI, including creation of a dedicated **Date table** to enable time intelligence calculations such as MTD and MoM.
- **Step 8 :** Using **DAX**, measures were written for the core KPIs required for Dashboard 1 (Summary):
  - Total Loan Applications, MTD Loan Applications, and MoM change in applications
  - Total Funded Amount, MTD Funded Amount, and MoM change in funded amount
  - Total Amount Received, MTD Amount Received, and MoM change in amount received
  - Average Interest Rate (overall and MTD), with MoM change
  - Average Debt-to-Income Ratio (DTI) (overall and MTD), with MoM change
- **Step 9 :** Loans were classified into **Good Loan** (Loan Status = "Fully Paid" or "Current") and **Bad Loan** (Loan Status = "Charged Off") categories using DAX, and matching KPI cards were created for each group:
  - Good/Bad Loan Application Percentage
  - Good/Bad Loan Applications
  - Good/Bad Loan Funded Amount
  - Good/Bad Loan Total Received Amount
- **Step 10 :** A **grid view** was built, categorised by **Loan Status**, showing Total Loan Applications, Total Funded Amount, Total Amount Received, MTD Funded Amount, MTD Amount Received, Average Interest Rate and Average DTI for each status — giving a single, comprehensive view of loan performance.
- **Step 11 :** For **Dashboard 2 (Overview)**, the following charts were built:
  - **Monthly Trends by Issue Date** (Line Chart) — to identify seasonality and long-term lending trends
  - **Regional Analysis by State** (Filled Map) — to identify regions with significant lending activity and regional disparities
  - **Loan Term Analysis** (Donut Chart) — to show the distribution of loans across different term lengths
  - **Employee Length Analysis** (Bar Chart) — to see how lending metrics vary with borrowers' employment history
  - **Loan Purpose Breakdown** (Bar Chart) — to understand the primary reasons borrowers seek financing
  - **Home Ownership Analysis** (Tree Map) — to see how home ownership status impacts loan applications and disbursements

  Each chart shows Total Loan Applications, Total Funded Amount and Total Amount Received.
- **Step 12 :** For **Dashboard 3 (Details)**, a consolidated grid was created giving a holistic, record-level view of key loan and borrower fields (Loan ID, Grade, Sub Grade, Purpose, Term, Interest Rate, DTI, etc.), acting as a one-stop reference for detailed loan-level insights.
- **Step 13 :** Card visuals, slicers (e.g. Grade, State, Loan Status, Purpose) and consistent formatting/theming were added across all three report pages, along with navigation buttons to move between the Summary, Overview and Details dashboards.
- **Step 14 :** The report was then published to **Power BI Service**.

### Fields used in the data

The dataset is built around the following key fields (as commonly used in bank loan analysis):

| Field | What it captures |
|---|---|
| Loan ID | Unique identifier for each loan, used to track it through its lifecycle |
| Address State | Borrower's location — used for regional risk and demand analysis |
| Employee Length | Borrower's length of employment — an indicator of income stability |
| Employee Title | Borrower's occupation, used to understand income source |
| Grade / Sub Grade | Risk classification assigned to the loan based on creditworthiness |
| Home Ownership | Borrower's housing status, an indicator of financial stability |
| Issue Date | Date the loan was originated |
| Last Credit Pull Date | Date the borrower's credit report was last checked |
| Last Payment Date | Date of the most recent loan payment |
| Loan Status | Current state of the loan — e.g. Fully Paid, Current, Charged Off |
| Next Payment Date | Expected date of the next payment, used for cash-flow forecasting |
| Purpose | Reason the loan was taken (e.g. debt consolidation, education) |
| Term | Duration of the loan, in months |
| Verification Status | Whether the borrower's financial information has been verified |
| Annual Income | Borrower's yearly income — used to assess repayment capacity |
| DTI (Debt-to-Income Ratio) | Borrower's debt burden relative to income |
| Instalment | Fixed monthly repayment amount |
| Interest Rate | Annual cost of borrowing, as a percentage |
| Loan Amount | Total principal amount borrowed |

# Snapshot of Dashboard (Power BI Service)

<img width="1905" height="901" alt="Screenshot 2026-08-11 023628" src="https://github.com/user-attachments/assets/96fbdc76-9943-400a-af10-12b57304fbb7" />


# Report Snapshot (Power BI Desktop)

<img width="1917" height="956" alt="Screenshot 2026-08-11 023600" src="https://github.com/user-attachments/assets/db5c135e-21b0-473d-9c46-4f0535a5f9ad" />

# Insights

A three-page report — **Summary**, **Overview** and **Details** — was built on Power BI Desktop, backed by SQL Server, and then published to Power BI Service.

The kind of inferences this dashboard is designed to surface include:

### [1] Loan Volume & Health (Summary Dashboard)

- Total Loan Applications, along with MTD and MoM movement, showing whether the pace of lending is accelerating or slowing.
- Total Funded Amount vs. Total Amount Received, showing how much of what was lent has actually come back — a direct read on collection performance.
- Average Interest Rate and Average DTI across the portfolio, showing how expensive the bank's lending is and how financially stretched its borrowers are, on average.

*(Total Applications = 38576, Total Funded Amount = $435.76M, Total Amount Received = $473.07M, Avg. Interest Rate = 12.07%, Avg. DTI = 13.33%.)*

### [2] Good Loan vs. Bad Loan

- The Good Loan vs. Bad Loan split (by application %, count, funded amount and received amount) shows what proportion of the lending book is healthy versus at risk of default.
- The Loan Status grid view breaks this down further, status by status, making it easy to spot which categories of loans need closer risk management.

*( Good Loan % = 86.18%, Bad Loan % = 13.82%)*

### [3] Regional & Segment Trends (Overview Dashboard)

- **Monthly trends** reveal whether lending activity is seasonal or growing steadily month over month.
- **State-wise analysis** highlights which regions drive the most lending activity, useful for regional risk management and targeted marketing.
- **Loan term, employment length, purpose and home ownership** breakdowns show which borrower segments the bank lends to most, and how those segments perform — informing which segments to grow and which to underwrite more cautiously.

### [4] Loan-Level Detail (Details Dashboard)

- The Details grid gives relationship managers and analysts a single place to look up any individual loan's status, terms and borrower profile, without needing to go back to the raw database.

### Functionalities used in this project

**SQL – MS SQL Server:** Creating Database, Creating Table, Select, Datename, Datepart, Cast, Decimal, Month, Hour, Quarter, Day, Group By, Order By, Limit, Count, Distinct, CTE, Partition.

**Power BI:** Connecting to SQL Server, Data Cleaning, Data Modelling, Data Processing, Power Query, Date Tables, Time Intelligence Functions, DAX, Date Functions, Text Functions, Filter Functions, Calculate, SUM/SUMX, Creating KPIs, Card Visuals, Creating Charts, Formatting Visuals, Creating Functions, Navigation.

### Software used

- MS Office / Excel — Version 2021
- MS SQL Server — 19.0
- SQL Server Management Studio — 19.0.20209.0
- Power BI — June 2023 version

### Why this analysis matters to the bank

Analysing loan data in this way supports several of the bank's core needs: **risk assessment** (evaluating creditworthiness and predicting defaults), **decision-making** (data-driven approval/denial of applications), **portfolio management** (spotting underperforming loans early), **fraud detection** (catching unusual patterns), **regulatory compliance** (e.g. HMDA, KYC reporting), **customer insights** (tailoring products to segments), **profitability analysis**, **market research**, **credit risk management**, and **customer retention**. This dashboard is built to serve all of these use cases from a single, consistent source of data.
