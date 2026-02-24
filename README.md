# 📊 Global Retail Sales Performance Dashboard – Power BI Project

## 📌 Project Overview

This Power BI dashboard analyzes the sales performance of a multinational retail company across different regions, product categories, customers, and time periods.

The objective is to help sales managers:

- Identify top-performing and underperforming products  
- Analyze seasonal and quarterly trends  
- Monitor key KPIs like Revenue, Profit Margin, and Growth  
- Optimize inventory and marketing strategies  
- Make data-driven business decisions  

---

## 🏗️ Data Model (Star Schema)

The project follows a **Star Schema** design:

### 🧾 Fact Table

#### Sales
- `SaleID`
- `ProductID` (FK → Products)
- `CustomerID` (FK → Customers)
- `Date` (FK → Dates)
- `Quantity`
- `Revenue`

---

### 📦 Dimension Tables

#### Products
- `ProductID`
- `ProductName`
- `Category`
- `Price`

#### Customers
- `CustomerID`
- `Name`
- `Region`

#### Dates
- `Date`
- `Month`
- `Quarter`
- `Year`

---

## 🔗 Relationships

- `Sales.ProductID → Products.ProductID` (Many-to-One)
- `Sales.CustomerID → Customers.CustomerID` (Many-to-One)
- `Sales.Date → Dates.Date` (Many-to-One)

✔ Dates table marked as Date Table  
✔ Single-direction filtering  
✔ Clean star schema model  

---

## 📊 Key Performance Indicators (KPIs)

- 💰 Total Revenue  
- 📦 Total Quantity Sold  
- 📈 Year-over-Year (YoY) Growth  
- 💹 Profit Margin  
- 👥 Average Revenue per Customer  
- 🌍 Revenue by Region  
- 🏷 Revenue by Category  

---

## 🧮 Important DAX Measures

```DAX
Total Revenue = SUM(Sales[Revenue])

Total Quantity = SUM(Sales[Quantity])

Average Revenue per Customer =
DIVIDE([Total Revenue], DISTINCTCOUNT(Customers[CustomerID]))

Previous Year Revenue =
CALCULATE([Total Revenue], SAMEPERIODLASTYEAR(Dates[Date]))

YoY Growth % =
DIVIDE([Total Revenue] - [Previous Year Revenue], [Previous Year Revenue])

Profit Margin % =
DIVIDE([Total Revenue] - SUMX(Sales, Sales[Quantity] * RELATED(Products[Price])), [Total Revenue])
