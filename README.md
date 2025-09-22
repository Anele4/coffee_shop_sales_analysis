
# ☕ Coffee Shop Sales Analysis

## 📌 Overview
This end-to-end project analyzes coffee shop sales data to uncover trends in product performance, customer behavior, and store-level metrics. Using SQL, Excel, Power Query, and Power BI, the dashboard delivers actionable insights for retail decision-makers and operational teams.

---

## 🎯 Objective
To transform raw transactional data into a dynamic dashboard that highlights key performance indicators, product category trends, and location-based performance for a coffee shop chain.

---

## 🛠️ Tools Used
- **SQL** – Data cleaning, KPI extraction, and time-based analysis  
- **Excel** – Preprocessing and validation  
- **Power Query** – Data transformation  
- **Power BI** – Dashboard design and visualization  
- **DAX** – KPI calculations and conditional formatting  
- **Python** – Exploratory analysis (optional mini projects)

---

## 📊 Key Metrics & Visuals

### 🔹 Top KPIs (May 2023)
- **Total Sales**: `$76.15K` (↓ 6.8% vs LM)
- **Total Orders**: `16,359` (↓ 5.5% vs LM)
- **Total Quantity Sold**: `23,550` (↓ 5.1% vs LM)

### 🔹 Product Category Breakdown
| Category     | Sales     |
|--------------|-----------|
| Coffee       | $42.4K    |
| Tea          | $11.3K    |
| Pastries     | $10.2K    |
| Sandwiches   | $7.2K     |
| Other        | $5.1K     |

### 🔹 Top Products (May 2023)
| Product       | Sales     |
|---------------|-----------|
| Espresso      | $12.3K    |
| Latte         | $10.2K    |
| Cappuccino    | $9.8K     |
| Green Tea     | $6.5K     |
| Croissant     | $5.7K     |

### 🔹 Store Performance
- **Downtown**: $35.2K  
- **Uptown**: $22.1K  
- **Suburb**: $18.8K

### 🔹 Weekday vs Weekend Sales
- **Weekday**: 76.5%  
- **Weekend**: 23.5%

### 📸 Screenshots
![Dashboard Overview]  <img width="953" height="559" alt="image" src="https://github.com/user-attachments/assets/e2ba2068-320d-4b1d-9d58-49230aa024d2" />
![Calander Tooltip]  <img width="239" height="181" alt="image" src="https://github.com/user-attachments/assets/c59d4a52-307f-4d3c-bc0f-594b4ce18a9f" />
![Day/Hour Tooltip]<img width="233" height="168" alt="image" src="https://github.com/user-attachments/assets/bcc8b7f7-6e44-497d-bb9f-404d200af1fd" />


---

## 🧮 SQL Queries Used

### 🔹 Data Cleaning
```sql
UPDATE coffee_shop_sales
SET transaction_date = STR_TO_DATE(transaction_date, '%d-%m-%Y');

ALTER TABLE coffee_shop_sales
MODIFY COLUMN transaction_date DATE;
```

### 🔹 KPI Calculations
```sql
SELECT ROUND(SUM(unit_price * transaction_qty)) AS Total_Sales
FROM coffee_shop_sales
WHERE MONTH(transaction_date) = 5;

SELECT COUNT(transaction_id) AS Total_Orders
FROM coffee_shop_sales
WHERE MONTH(transaction_date) = 5;

SELECT SUM(transaction_qty) AS Total_Quantity_Sold
FROM coffee_shop_sales
WHERE MONTH(transaction_date) = 5;
```

### 🔹 Month-over-Month Growth
```sql
SELECT
  MONTH(transaction_date) AS month,
  ROUND(SUM(unit_price * transaction_qty)) AS total_sales,
  (SUM(unit_price * transaction_qty) - LAG(SUM(unit_price * transaction_qty), 1)
   OVER (ORDER BY MONTH(transaction_date))) / LAG(SUM(unit_price * transaction_qty), 1)
   OVER (ORDER BY MONTH(transaction_date)) * 100 AS mom_increase_percentage
FROM coffee_shop_sales
WHERE MONTH(transaction_date) IN (4, 5)
GROUP BY MONTH(transaction_date)
ORDER BY MONTH(transaction_date);
```

### 🔹 Daily Sales vs Average
```sql
SELECT
  DAY(transaction_date) AS day_of_month,
  SUM(unit_price * transaction_qty) AS total_sales,
  AVG(SUM(unit_price * transaction_qty)) OVER () AS avg_sales
FROM coffee_shop_sales
WHERE MONTH(transaction_date) = 5
GROUP BY DAY(transaction_date);
```

### 🔹 Sales by Day Type
```sql
SELECT
  CASE
    WHEN DAYOFWEEK(transaction_date) IN (1, 7) THEN 'Weekend'
    ELSE 'Weekday'
  END AS day_type,
  ROUND(SUM(unit_price * transaction_qty), 2) AS total_sales
FROM coffee_shop_sales
WHERE MONTH(transaction_date) = 5
GROUP BY day_type;
```

### 🔹 Sales by Store Location
```sql
SELECT store_location,
       SUM(unit_price * transaction_qty) AS Total_Sales
FROM coffee_shop_sales
WHERE MONTH(transaction_date) = 5
GROUP BY store_location
ORDER BY Total_Sales DESC;
```

---

## 🧠 Insights & Takeaways
- **Espresso and Latte** are the top-performing products, driving over 25% of total sales.
- **Weekday traffic** dominates, suggesting strong commuter or workday demand.
- **Downtown store** leads in revenue, but shows signs of month-over-month decline.
- **Pastries and Sandwiches** perform better during weekends and late mornings.

---

## ✨ Lessons Learned
- How to clean and format time-series data using SQL
- Designing calendar views and heatmaps in Power BI
- Using DAX to calculate dynamic KPIs and MoM comparisons
- Building storytelling visuals that guide business decisions

---

## 👤 About Me

I’m Anele, a BSc Applied Food & Tech graduate who pivoted into data analytics to solve real-world problems with precision and creativity. After completing a data analyst/scientist course, I delivered end-to-end client projects using SQL, Excel, Power Query, and Power BI—transforming raw data into actionable dashboards. I’ve also built Python mini-projects for data cleaning and visualization.

My passion lies in making insights beautiful and impactful. I blend technical logic with design aesthetics to create dashboards that not only inform but inspire action. I’m currently open to freelance roles and independent contracts where I can help businesses turn data into clarity.

---

## 🔗 Connect With Me

- **LinkedIn**: [Anele Promise Ndlovu](https://www.linkedin.com/in/anele-promise-ndlovu-6a8586277)  
- **GitHub**: [Anele4](https://github.com/Anele4)
```
