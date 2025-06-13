# Zomato Data Project

This repository contains SQL scripts and examples for creating, populating, and querying a Zomato restaurants dataset. It includes:

- **zomato_data**: main table with restaurant details  
- **calendar_table**: derived calendar dimensions based on opening dates  
- **CurrencyExchange**: reference table for currency conversion rates  

---

## Table Structures

### `zomato_data`

| Column                   | Type               | Description                                   |
| ------------------------ | ------------------ | --------------------------------------------- |
| RestaurantID             | INT                | Unique identifier for each restaurant         |
| RestaurantName           | VARCHAR(255)       | Name of the restaurant                        |
| CountryCode              | INT                | Numeric country code                          |
| Country_Name             | VARCHAR(100)       | Full country name                             |
| City                     | VARCHAR(100)       | City where the restaurant is located          |
| Address                  | VARCHAR(255)       | Street address                                |
| Locality                 | VARCHAR(100)       | Neighborhood or locality                      |
| LocalityVerbose          | VARCHAR(255)       | Detailed locality description                 |
| Longitude, Latitude      | FLOAT              | Geographic coordinates                        |
| Cuisines                 | VARCHAR(255)       | Comma-separated list of cuisines offered      |
| Currency                 | VARCHAR(50)        | Currency used for cost values                 |
| Has_Table_booking        | BOOLEAN            | `1` if table booking available, else `0`      |
| Has_Online_delivery      | BOOLEAN            | `1` if online delivery available, else `0`    |
| Is_delivering_now        | BOOLEAN            | `1` if currently delivering, else `0`         |
| Switch_to_order_menu     | BOOLEAN            | `1` if “Order” menu enabled, else `0`         |
| Price_range              | INT                | Price range category (e.g. 1–4)               |
| Votes                    | INT                | Number of user votes                          |
| Average_Cost_for_two     | INT                | Average cost for two people                   |
| Rating                   | DECIMAL(3,2)       | Average user rating (0.00–5.00)               |
| Datekey_Opening          | DATE               | Opening date (DD-MM-YYYY converted to DATE)   |

### `calendar_table`

Derived dimension table for date-based analysis:

| Column           | Type    | Description                                   |
| ---------------- | ------- | --------------------------------------------- |
| DateKey          | DATE    | Date of opening                               |
| Year             | INT     | Year part                                     |
| MonthNo          | INT     | Month number (1–12)                           |
| MonthFullName    | VARCHAR | Full month name (e.g. January)                |
| YearMonth        | VARCHAR | Year and abbreviated month (e.g. “2025-Jun”)  |
| Quarter          | INT     | Calendar quarter (1–4)                        |
| WeekdayNo        | INT     | Day of week (1=Sunday…7=Saturday)             |
| WeekdayName      | VARCHAR | Name of the weekday                           |
| FinancialMonth   | VARCHAR | Financial month code (FM1–FM12)               |
| FinancialQuarter | VARCHAR | Financial quarter code (FQ1–FQ4)              |

### `CurrencyExchange`

Reference rates to convert to USD and INR:

| Column            | Type         | Description                              |
| ----------------- | ------------ | ---------------------------------------- |
| Currency          | VARCHAR(50)  | Name and symbol of currency              |
| ExchangeRateToUSD | DECIMAL(10,6)| Rate to convert 1 unit to USD            |
| Code              | VARCHAR(10)  | Currency code (e.g. INR, USD, GBP)       |

---

## SQL Scripts

A concise collection of SQL scripts is available to:

- Create and configure the main Zomato tables (`zomato_data`, `calendar_table`, `CurrencyExchange`).  
- Load raw CSV data into MySQL (via `LOAD DATA INFILE`).  
- Populate derived tables and reference rates.  

*(See `zomato_Analysis_MYSQL.sql` for full scripts.)*

---

## Power BI Dashboard Overview

The companion Power BI report is organized into six pages, each presenting key insights and interactive filters:

### 1. Home
- **Global KPIs**: YOY Growth %, Previous Year Sales, Total Sales ($ & ₹), Total Restaurants, Distinct Cuisines, Total Countries & Cities, Average Rating, Total Votes.  
- **Year-over-Year Trend**: Growth % by Year & Quarter.  
- **Distribution Charts**: Restaurants by Rating; Count of Restaurants by Opening Date; Top 10 Cuisines.

### 2. Dashboard
- **Year Selector**: Clear & Filter buttons for quick resets.  
- **Filtered KPIs**: YOY Growth %, Previous Year Sales, Total Sales for selected year.  
- **Gauge**: Total Sales relative to full range.  
- **Visuals**: YOY growth bar-waterfall by Year; Total Sales by Financial Month & Calendar Month; Count of Restaurants by Financial Quarter & Month.

### 3. Year
- **Year-to-Date KPIs**: YOY Growth %, Previous Sales, Total Sales.  
- **Trends**: Sales by Financial Month; Sales by Calendar Month.  
- **Breakdowns**: Count of Restaurants by Financial Quarter & Month.

### 4. Cuisines
- **Top Cuisines**: Count of Restaurants for Top 10; Top 5 Sales by Cuisine.  
- **Quality & Geography**: Count of Cuisines by Rating (emoji faces); Top 5 Cuisines by Country.

### 5. Country
- **Country Selector**: Clear & Filter controls.  
- **Sales Map**: Geo-map of Sales (enable in File > Options > Global > Security).  
- **KPIs**: Total Sales by City & Country.  
- **Trend**: Sales for selected country by City.

### 6. Rating
- **Performance by Rating**: Total Sales line chart across rating categories (emoji faces).  
- **Restaurant Counts**: Bar chart of count by rating.  
- **Rating vs Votes**: Scatter plot showing correlation between votes and ratings.

---

Feel free to explore each page interactively in the Power BI `.pbix` file to uncover deeper insights!  
