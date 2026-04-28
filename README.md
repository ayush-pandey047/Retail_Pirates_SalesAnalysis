# Retail Sales Performance Analysis

## Project Overview
This project implements an end-to-end data analytics pipeline to analyse retail transaction data and extract actionable insights. The workflow transforms raw data into a clean, structured dataset and supports analysis through feature engineering and visualisation.

The pipeline is divided into three stages: Extraction, Cleaning, and ETL/Feature Engineering.

---

## Dataset
- Source: `data/raw/retail_store_sales.csv`
- Records: ~12,575 transactions
- Time Period: January 2022 – January 2025
- Customers: 25
- Categories: 8
- Payment Methods: Cash, Credit Card, Digital Wallet

### Key Fields
Transaction ID, Customer ID, Category, Item, Price Per Unit, Quantity, Total Spent, Payment Method, Location, Transaction Date, Discount Applied

---

## Data Pipeline

### 1. Extraction
- Load dataset using Pandas
- Inspect structure, data types, and summary statistics
- Identify missing values and duplicates

### 2. Cleaning
- Remove duplicate records
- Handle missing values:
  - Numerical → median
  - Categorical → mode
- Convert transaction date to datetime
- Standardise column names
- Remove outliers using IQR method (157 rows removed)
- Export cleaned dataset

### 3. ETL & Feature Engineering
- Time features: year, month, quarter, day_of_week
- revenue_per_unit
- is_bulk flag
- spent_segment (Low / Medium / High)
- discount_flag
- category_code

---

## Tech Stack
- Python 3
- Pandas
- NumPy
- Matplotlib
- Jupyter Notebook

---

## Key Insights
- Sales are concentrated in a small number of product categories
- High-value customers contribute a disproportionate share of revenue
- ~33% of discount data is missing, limiting discount analysis
- Payment preferences vary across locations
- Bulk transactions are fewer but have higher transaction value
- Dataset has limited customer diversity (25 customers)

---

## Dashboards
- Executive Summary:  
  https://public.tableau.com/app/profile/pranay.chitare/viz/RetailPiratesSalesAnalysis/ExecutiveSummary

- Operational Drill-Down:  
  https://public.tableau.com/app/profile/pranay.chitare/viz/RetailPiratesSalesAnalysis/OperationalDrill-Down

---

## Project Structure
