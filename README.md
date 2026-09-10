# E-Commerce Sales Analysis

End-to-end analysis of e-commerce transaction data — from raw orders to a star-schema data model and an interactive Power BI dashboard — built to support sales, profitability, and customer-behavior decisions.

## Project Overview

E-commerce businesses generate large volumes of transactional data, but raw data alone rarely drives decisions. This project turns raw order and product-level data into actionable insight through data cleaning, exploratory data analysis (EDA), dimensional modeling, and an interactive Power BI dashboard.

**Objectives**
- Analyze overall sales and profitability performance
- Identify best- and worst-performing product categories/sub-categories
- Analyze sales and profit trends over time
- Evaluate geographic sales and profitability performance
- Understand customer purchasing behavior and payment method performance
- Identify loss-making product segments and locations
- Transform raw transactional data into an optimized Star Schema
- Build an interactive Power BI dashboard for business decision-making

## Dataset

The dataset covers 1,500 transaction-level records (500 unique orders) with order, product, customer, location, date, quantity, sales amount, profit, and payment-method information. `Orders.csv` and `Details.csv` are joined on `Order ID` and cleaned/validated (no missing values, no duplicate records).

## Workflow

1. **Data cleaning & EDA** (`notebooks/EDA.ipynb`) — merge orders/details, validate types and duplicates, descriptive statistics, outlier and correlation analysis
2. **Dimensional modeling** — transformed into a Star Schema for Power BI
3. **DAX measures** — KPI and business-logic calculations
4. **Dashboard** — 4-page interactive Power BI report

### Key EDA Findings
- No missing values or duplicate records
- Average order amount: 291.85 | Average profit: 24.64 | Average quantity: 3.74
- Amount and Quantity show the strongest correlation (0.352) — still weak-to-moderate; profitability is not driven by volume alone
- Clothing has the highest transaction count among categories
- COD is the most common payment method
- Madhya Pradesh and Maharashtra lead in transaction activity

## Data Model — Star Schema

**Fact table:** `FactDetails` (Order ID, Order Date, Customer ID, Location ID, Product ID, Payment ID, Amount, Profit, Quantity)

**Dimensions:** `DateDim`, `ProductDim` (Category, Sub-Category), `LocationDim` (City, State), `CustomerDim`, `PaymentDim`

## DAX Measures

| Measure | Logic |
|---|---|
| Total Sales | `SUM(FactDetails[Amount])` |
| Total Profit | `SUM(FactDetails[Profit])` |
| Total Orders | `DISTINCTCOUNT(FactDetails[Order ID])` |
| Total Customers | `DISTINCTCOUNT(FactDetails[CustomerID])` |
| Profit Margin | `DIVIDE([Total Profit], [Total Sales], 0)` |
| Average Order Value | `DIVIDE([Total Sales], [Total Orders], 0)` |
| Repeat Customer Rate | Customers with >1 order ÷ Total Customers |
| Loss-Making Sub-Categories / States | Count of dimension members where `[Total Profit] < 0` |
| Top City/State Sales, Top State Profit | `TOPN`-based ranking measures |

## Dashboard

Four analytical pages built in Power BI:

1. **Sales Performance** — Total Sales, Profit, Orders, Quantity; monthly sales trend; sales by state/category/payment mode
2. **Product & Profitability** — AOV, average profit per order, loss-making sub-categories; sales & profit trend by month; profit margin by category/sub-category
3. **Geographic Performance** — state/city-level sales and profitability
4. **Customer & Payment Behavior** — repeat customer rate, payment method distribution

## Tech Stack

- **Python** (pandas, NumPy, Matplotlib) — data cleaning & EDA
- **Power BI** — data modeling (Star Schema), DAX, dashboard
- **Jupyter Notebook**

## Repository Structure
