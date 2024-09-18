# FINANCIAL HEALTH ANALYSIS PORTFOLIO


![SEC DASH BOARD](Images/SEC3_Logo.png)
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
    - 4.6 [Data Visualization & Dashboard Mockup](#data-visualization--dashboard-mockup)
5. [Recommendations](#recommendations)
6. [Issues and Amendments](#issues-and-amendments)
7. [Future Work](#future-work)
8. [Contact](#contact)

## Introduction
We are an independent institution providing stakeholders with insights and analysis of public company financial data. Our goal is to help investors, corporate strategy teams, and other stakeholders make informed decisions regarding investment opportunities in the U.S. public market. This project leverages financial data from SEC EDGAR to generate reports, predictions, and dashboards.

## Objective
To provide comprehensive analysis and visual representation of financial data from public companies in the U.S. This includes financial performance analysis, forecast modeling, and comparisons across sectors, enabling stakeholders to make data-driven investment decisions.

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
- **Source**: SEC EDGAR via API.
- **Tools**: Python for API requests, Power Query for URL-based data ingestion.
 
- **Steps**:
    1. Extract financial statements for quarterly (10-Q) and annual (10-K) filings.
    2. Utilize company-specific identifiers (CIK) for precise data retrieval.
    3. Data is stored in CSV format
       
```python
# Example Python script to extract data using SEC EDGAR API
import requests
api_url = "https://www.sec.gov/edgar/xbrl"
response = requests.get(f"{api_url}/cik/{company_id}/financials")
```

### 4.2 Data Cleaning
- **Tools**: Python (pandas), Power Query.
  
- **Steps**:
     1. Remove null and duplicate data.
     2. Validate and standardize financial metrics.
     3. Ensure consistent date formatting (Quarterly and Annual).
     4. Processed data will be stored in the data/processed/ directory.

### 4.3 Data Storage
- **Database**: PostgreSQL.
  
- **Steps**:
      1. create tables for each financial statement (Income Statement, Balance Sheet, Cash Flow).
      2. Load cleaned data into PostgreSQL to support scalable querying and analysis.

- **CREATE TABLE balance_sheet (
    cik VARCHAR(10),
    period DATE,
    total_assets NUMERIC,
    total_liabilities NUMERIC
)**;

### 4.4 Exploratory Data Analysis (EDA)
- **Tools**: Python (pandas, seaborn), SQL queries via PostgreSQL.
  
- **Steps**:
    1. Conduct historical financial analysis (revenue growth, net income trends).
    2. Analyze sector performance, highlighting top-performing and underperforming companies.
    3. Visualize financial metrics using graphs and charts for key insights.

### 4.5 Analysis & KPIs
- **Tool**s: Power BI, DAX for KPI calculation.
  
- **KPIs**:
    1. Revenue Growth: Measure year-over-year revenue changes.
    2. Net Profit Margin: Calculate the ratio of net income to total revenue.
    3. Filing Punctuality: Track company filing history and punctuality.

DAX Calculations in Power BI:

Revenue Growth = 
DIVIDE(
  SUM('Financials'[Revenue]) - CALCULATE(SUM('Financials'[Revenue]), PREVIOUSYEAR('Financials'[Year])),
  CALCULATE(SUM('Financials'[Revenue]), PREVIOUSYEAR('Financials'[Year]))
)
Net Profit Margin = 
DIVIDE(SUM('Financials'[Net Income]), SUM('Financials'[Revenue]))

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

Best Performing Companies: Identify companies with consistent revenue growth and strong profitability metrics.
Sector Insights: Analyze which sectors are outperforming and high
light high-potential companies within each sector.
Risk Indicators: Highlight companies with irregular filing patterns or deteriorating financials.
    
To be expanded as analysis progresses.


# Issues and Amendments
To be expanded as analysis progresses.

