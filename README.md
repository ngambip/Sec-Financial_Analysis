# FINANCIAL HEALTH ANALYSIS

![SEC DASH BOARD](Images/SEC2_Logo.png)
---

## Table of Contents
1. [Introduction](#introduction)
2. [Objective](#objective)
3. [Deliverables](#deliverables)
4. [Process Overview](#process-overview)
    - 4.1 [Data Extraction](#data-extraction)
    - 4.2 [Data Cleaning](#data-cleaning)
    - 4.3 [Data Storage](#data-storage)
    - 4.4 [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
    - 4.5 [Analysis & KPIs](#analysis--kpis)
    - 4.6 [Data Visualization](#data-visualization)
5. [Recommendations](#recommendations)
6. [Issues and Updates](#issues-and-updates)
7. [Contact](#contact)

## Introduction
This project is aimed at providing investors and corporate strategy teams with insights into the best public companies in the US for investment. We audit and analyze financial statements to evaluate past performance, forecast future performance, and generate sector comparisons.

## Objective
To assist investors in identifying the best companies for investment and support corporate strategy teams by analyzing and auditing financial statements for due diligence purposes.

## Deliverables
- **Financial Statements Recreated in Excel**
    - Income Statement
    - Balance Sheet
    - Cash Flow Statement
    - Statement of Changes in Equity
- **Reports** containing:
    - Historical and predicted financial performance
    - Filing history and punctuality
    - Best/worst-performing companies per sector
- **Dashboards** showcasing key financial metrics via Power BI, Tableau, or Looker.

## Process Overview

### 4.1 Data Extraction
- **Source**: SEC EDGAR via the XBRL API.
- **Tools**: Python for API requests, Power Query for URL downloads.
- **Process**:
    1. Extract financial data (Income Statement, Balance Sheet, Cash Flow) for quarterly (10-Q) and annual (10-K) filings.
    2. Company-specific identifiers such as CIK will be used for targeted data extraction.
    3. Data is initially stored in CSV format before further processing.

### 4.2 Data Cleaning
- **Tools**: Python (pandas), Power Query.
- **Steps**:
    1. Remove any null or missing values.
    2. Format dates and ensure consistent time periods.
    3. Validate financial metrics across different periods for consistency.
    4. Store cleaned data in the `processed/` directory.
    
    ```python
    # Example: Data Cleaning using Python
    df.dropna(subset=['revenue', 'net_income'], inplace=True)
    df['date'] = pd.to_datetime(df['date'])
    ```
    
### 4.3 Data Storage
- **Database**: PostgreSQL
- **Process**:
    1. Create tables for each financial statement (Income Statement, Balance Sheet, Cash Flow).
    2. Store cleaned data into PostgreSQL for efficient querying and scalability.
    
    ```sql
    CREATE TABLE income_statement (
        cik VARCHAR(10),
        period DATE,
        revenue NUMERIC,
        net_income NUMERIC
    );
    ```

### 4.4 Exploratory Data Analysis (EDA)
- **Tools**: Python (matplotlib, seaborn), SQL queries from PostgreSQL.
- **Process**:
    1. Analyze past financial performance by reviewing revenue growth, profitability, and cash flow.
    2. Generate sector-wise analysis for top and bottom performers.
    3. Visualize trends such as revenue growth, net income, and balance sheet ratios.
    
    ```python
    # Example: EDA for revenue growth
    sns.lineplot(data=df, x='date', y='revenue', hue='company_sector')
    ```

### 4.5 Analysis & KPIs
- **Tools**: Power BI, DAX for KPI calculation.
- **Key Metrics**:
    - Revenue Growth
    - Earnings Before Interest & Taxes (EBIT)
    - Net Profit Margin
    - Filing punctuality rates
    - Best/Worst performers per sector
    
    **DAX Calculations in Power BI**:
    
    - **Revenue Growth**:
    ```DAX
    Revenue Growth = (SUM('Financials'[Revenue]) - CALCULATE(SUM('Financials'[Revenue]), PREVIOUSYEAR('Financials'[Year]))) / CALCULATE(SUM('Financials'[Revenue]), PREVIOUSYEAR('Financials'[Year]))
    ```

    - **Net Profit Margin**:
    ```DAX
    Net Profit Margin = DIVIDE(SUM('Financials'[Net Income]), SUM('Financials'[Revenue]))
    ```

    - **Filing Punctuality**:
    ```DAX
    Filing Punctuality = DIVIDE(SUM('Filings'[On Time Filings]), COUNTROWS('Filings'))
    ```

### 4.6 Data Visualization
- **Tools**: Power BI, Tableau, Looker
- **Visuals**:
    - **Income & Expense Analysis**: Revenue and expense breakdown for each company.
    - **Growth Analysis**: Visuals showing revenue, earnings, and profitability over time.
    - **Competitor Analysis**: Comparisons of key metrics (e.g., revenue, profit) across companies in the same sector.
    - **Filing History**: Visual representation of on-time vs late filings.
    - **Predictions**: Forecasting visualizations for revenue, cash flow, and net income.
    
    ```DAX
    Revenue Forecast = FORECAST.ETS('Financials'[Revenue], 'Financials'[Date], 12, 0.95)
    ```

## Recommendations
- **Best Investment Opportunities**: Based on analysis, recommend companies with strong financial growth, positive profitability trends, and timely filings.
- **Sector Insights**: Highlight the sectors with consistent performers and those with volatile financials.
- **Risk Assessment**: Flag companies with inconsistent filings or negative financial growth for further review.

## Issues and Updates
This section will track ongoing issues and updates as they arise during the project. New issues will be documented here with steps taken for resolution.

- **Issue 1**: API rate limits on SEC EDGAR—resolved by implementing batch requests.
- **Issue 2**: Power BI DAX calculation errors—pending review.

## Contact
For any questions or collaboration opportunities, please contact:

- **Project Lead**: [Your Name]
- **Email**: [Your Email]
- **Phone**: [Your Contact Number]
