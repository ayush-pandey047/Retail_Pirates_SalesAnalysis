Project Overview:
A data analytics pipeline built in Python/Jupyter notebooks that processes retail store transaction data through three stages: Extraction, Cleaning, and ETL/Feature Engineering.

Dataset:
Source: data/raw/retail_store_sales.csv
Size: ~12,500 transactions
Time Period: January 2022 – January 2025
Columns: Transaction ID, Customer ID, Category, Item, Price Per Unit, Quantity, Total Spent, Payment Method, Location, Transaction Date, Discount Applied


Pipeline Stages:

1. Extraction: Load raw CSV, inspect shape, columns, data types, memory usage, descriptive statistics, missing values, duplicates, and unique values.

2. Cleaning: Remove duplicates, impute missing values (median for numeric, mode for categorical), convert date column, standardize column names, remove outliers using IQR method, export cleaned data to data/processed/cleaned_data.csv.

3. ETL & Feature Engineering: Extract year, month, quarter, day of week from transaction date; calculate revenue per unit; create is_bulk flag; create spent_segment (Low/Medium/High); create discount_flag; create category_code; export final DataFrame.