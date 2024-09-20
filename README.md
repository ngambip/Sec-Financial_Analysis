# FINANCIAL HEALTH ANALYSIS PORTFOLIO


![SEC DASH BOARD](Images/SEC3_Logo.png)
---

## Table of Contents
1. [Introduction](#introduction)
2. [Objective](#objective)
3. [Deliverables](#deliverables)
4. [Process Overview](#process-overview)
    - 4.1 [Data Extraction](#data-extraction)
    - 4.2 [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)- 
    - 4.3 [Data Cleaning](#data-cleaning)
    - 4.4 [Data Storage](#data-storage)
 
    - 4.5 [Analysis & KPIs](#analysis--kpis)
    - 4.6 [Data Visualization & Dashboard Mockup](#data-visualization--dashboard-mockup)
5. [Recommendations](#recommendations)
6. [Issues and Amendments](#issues-and-amendments)


## Introduction
Our project objective is to analyze and visualize financial data from U.S. public companies, providing clear insights and forecasts to help stakeholders make informed investment decisions.

## Objective
- **Our services include**:
    - Analyzing financial data
    - Offering financial advice based on expert reports
    - Educating clients through data-driven insights
    - Developing financial models to predict future trends
    - Benchmarking company performance against industry standards
    - Creating custom financial dashboards for real-time tracking
    - Conducting risk assessments to identify potential financial challenges
    - Offering tailored investment recommendations based on data analysis.

## Deliverables

- **Financial Statements** recreated in Excel:
    - Income Statement
    - Balance Sheet
    - Cash Flow Statement
    - Statement of Changes in Equity
    - 
- **Financial Reports** on:
    - Past financial performance
    - Predicted performance
    - Filing history and punctuality
    - Sector-based best/worst performance
     
- **Dashboards** showcasing key metrics using Power BI, Tableau, or Looker, including:
    - Income & Expense Analysis
    - Growth Analysis
    - Competitor Analysis
    - Filing History
    - Performance Predictions

## Process Overview

### 4.1 Data Extraction
- **Source**: SEC EDGAR
- **Tools**: Python for API requests, Power Query for URL-based data ingestion.
 
- **Steps**:
    1. Extract financial statements for quarterly (10-Q) and annual (10-K) filings.
    2. Utilize company-specific identifiers (CIK) for precise data retrieval.
    3. Data is stored in CSV and JSON format
       
```python
# Example Python script to extract data using SEC EDGAR API
import requests
api_url = "https://www.sec.gov/edgar/xbrl"
response = requests.get(f"{api_url}/cik/{company_id}/financials")
```
### 4.2 Exploratory Data Analysis (EDA)
- **Tools**: Python (pandas, seaborn), SQL queries via PostgreSQL.
  
- **Steps**:
   1.  Inspect column names and data types
   2.  Check summary statistics (mean, median, mode, etc.)
   3.  Analyze frequency distributions for categorical data
   4.  Identify missing or null values
   5.  Visualize data distributions using histograms, box plots, or density plots
   6.  Detect outliers with scatter plots or box plots
   7.  Explore variable relationships using scatter plots or correlation matrices
   8.  Evaluate data quality based on initial observations
   9.  Note any potential data type mismatches or unrealistic values
  10.  Look for duplicate entries in the data
  11.  Conduct historical financial analysis (revenue growth, net income trends).
  12.  Analyze sector performance, highlighting top-performing and underperforming companies.
  13.  Visualize financial metrics using graphs and charts for key insights.

### 4.3 Data Cleaning
- **Tools**: Python (pandas), Excel (Power Query).
  
- **Steps**:
     1. Remove null and duplicate data.
     2. Validate and standardize financial metrics.
     3. Ensure consistent date formatting (Quarterly and Annual).
     4. Processed data will be stored in the data/processed/ directory.

### 4.4 Data Storage
- **Database**: PostgreSQL.
  
- **Steps**:
    1. create tables for each financial statement (Income Statement, Balance Sheet, Cash Flow).
    2. Load cleaned data into PostgreSQL to support scalable querying and analysis.

 ```sql
  CREATE TABLE balance_sheet (
    cik VARCHAR(10),
    period DATE,
    total_assets NUMERIC,
    total_liabilities NUMERIC
)**;
```

### 4.5 Analysis & KPIs
- **Tool**s: Power BI, DAX for KPI calculation.
  
- **KPIs**:
    1. Revenue Growth: Measure year-over-year revenue changes.
    2. Net Profit Margin: Calculate the ratio of net income to total revenue.
    3. Filing Punctuality: Track company filing history and punctuality.

DAX Calculations in Power BI:

```sql
Revenue Growth = 
DIVIDE(
  SUM('Financials'[Revenue]) - CALCULATE(SUM('Financials'[Revenue]), PREVIOUSYEAR('Financials'[Year])),
  CALCULATE(SUM('Financials'[Revenue]), PREVIOUSYEAR('Financials'[Year]))
)
```

```sql
Net Profit Margin = 
DIVIDE(SUM('Financials'[Net Income]), SUM('Financials'[Revenue]))

```

### 4.6 Data Visualization & Dashboard Mockup
- **Tools**: Power BI, Tableau, or Looker.
  
- **Mockup Design**: This dashboard will provide interactive and visual insights into financial performance.

### Dashboard Sections:
- Income & Expense Analysis:
  Visualize key metrics like Revenue, Net Income, Expenses over time.
        
- Growth Analysis:
  Show quarterly and annual growth rates of revenue, income, and key financial ratios.
        
- Competitor Analysis:
  Comparison of company performance within sectors to identify top performers.
        
- Filing History:
  A timeline visualization showing punctual and delayed filings for each company.
        
Performance Predictions:
Forecast future financial performance based on historical trends using predictive models.


# Recommendations

- Best Performing Companies: Identify companies with consistent revenue growth and strong profitability metrics.
- Sector Insights: Analyze which sectors are outperforming and high
- light high-potential companies within each sector.
- Risk Indicators: Highlight companies with irregular filing patterns or deteriorating financials.
    
To be expanded as analysis progresses.


# Issues and Amendments
To be expanded as analysis progresses.

