# Customer Net Sales Analytics and Market Performance Report

This repository contains a detailed analysis of customer net sales and market performance versus targets, conducted using Excel tools such as Power Query, Power Pivot, and Pivot Tables. The project covers the extraction, transformation, and visualization of data to derive insights into customer and market trends for AtliQ Hardware.

## Project Overview

The project involves the integration of five datasets to create a comprehensive report analyzing sales performance, customer behavior, and market trends. The data spans multiple dimensions, including customers, products, markets, and sales performance, with a focus on fiscal years 2019 to 2021.

## Datasets

### 1. **dim_customer**
   - Details of customers, including:
     - `customer_code`
     - `customer_name` (company)
     - `market` (country)
     - `platform` (Brick & Mortar/E-commerce)
     - `channel` (Distributor/Direct/Retailer)

### 2. **dim_market**
   - Market information, including:
     - `market` (country)
     - `subzone` (e.g., NE, NAN, India)
     - `region` (e.g., NAN, EU, APAC)

### 3. **dim_product**
   - Product details:
     - `product_code`
     - `division` (e.g., N&S, PC, P&A)
     - `segment` (e.g., Accessories, Desktop)
     - `category`, `product`, `variant`

### 4. **fact_sales_monthly**
   - Monthly sales data:
     - `date`
     - `product_code`
     - `customer_code`
     - `QTY`
     - `net_sales_amount`

### 5. **ns_target_2021**
   - Sales targets for 2021:
     - `market` (country)
     - `date`
     - `ns_target`

## Data Preparation

### ETL Process
1. **Data Extraction**:
   - Imported all datasets into Power Query.

2. **Data Transformation**:
   - **dim_customer**: Cleaned inconsistent customer names.
   - **dim_market**: Corrected `nan` values to `NA` (North America).
   - **fact_sales_monthly**:
     - Converted negative QTY values to absolute values.
     - Created `new_date_modified` column to standardize date formats.
   - **dim_date**: Created a custom fiscal year calendar (SEP-AUG).

3. **Data Loading**:
   - Loaded transformed data into Power Pivot in data model and connection mode.

### Relationships in Power Pivot
- **dim_customer** ➡ fact_sales_monthly (`customer_code`)
- **dim_product** ➡ fact_sales_monthly (`product_code`)
- **dim_date** ➡ fact_sales_monthly (`new_date_modified`)
- **dim_date** ➡ ns_target_2021 (`date`)
- **dim_market** ➡ ns_target_2021 (`market`)
- **dim_market** ➡ dim_customer (`market`)

## Measures and Calculations

- **Net Sales**: `SUM(fact_sales_monthly[net_sales_amount])`
- **Net Sales (Year)**: `CALCULATE([Net Sales], dim_date[FY year] = "YYYY")`
- **Year-on-Year Growth**: `DIVIDE([Net Sales 21], [Net Sales 20], 0)`
- **Target Achievement**: `[Net Sales 21] - [Target 21]`

## Visualization

- Created Pivot Tables and conditional formatting for enhanced readability.
- Analyzed key metrics, including:
  - Net Sales growth for customers (2019–2021)
  - Market performance versus targets in 2021
  - Trends by region, division, and segment

## Key Insights

1. **Customer Growth**:
   - Significant growth in key accounts like Amazon and AtliQ Exclusive (e.g., Amazon's sales grew by 218.87% from 2020 to 2021).

2. **Market Trends**:
   - Markets like India and USA showed robust sales but missed targets by 5.9% and 11.7%, respectively.

3. **Product Performance**:
   - Divisions like N&S and PC contributed significantly to sales growth.



## Getting Started

1. Open the Power Query Editor in Excel to explore the ETL process.
2. Use Power Pivot Diagram View to review table relationships.
3. Review Pivot Table reports for sales performance and market insights.

## Prerequisites

- Microsoft Excel with Power Query and Power Pivot enabled.
- Basic understanding of ETL processes and Pivot Table creation.

## Contributing

Feel free to fork this repository, submit issues, or propose improvements to the analysis process or visualizations.
