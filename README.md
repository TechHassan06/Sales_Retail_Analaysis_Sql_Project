# Retail Sales Analysis – SQL Project

## Project Overview

**Project Title:** Retail Sales Analysis
**Level:** Beginner to Intermediate
**Tools Used:** SQL
**Database:** `retail_sales`

This project demonstrates practical SQL skills used in real-world data analysis. The dataset contains retail sales transactions including customer details, product categories, purchase quantities, and sales values.

The objective of this project is to clean the dataset, perform exploratory data analysis (EDA), and answer important business questions using SQL queries. This project highlights how SQL can be used to generate meaningful insights from retail transaction data.

---

# Project Objectives

The main goals of this project are:

1. **Create a Retail Sales Database**
   Build a structured table to store retail transaction data.

2. **Data Cleaning**
   Identify and remove records containing missing or null values to ensure data quality.

3. **Exploratory Data Analysis (EDA)**
   Understand the structure of the dataset by examining customers, categories, and transactions.

4. **Business Insights Using SQL**
   Analyze the data and answer business questions related to sales performance and customer behavior.

---

# Database Structure

The project uses a table called **`retail_sales`** which stores all transaction data.

### Table Schema

```sql
CREATE TABLE retail_sales(
    transaction_id INT,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(10),
    age INT,
    category VARCHAR(15),
    quantity INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);
```

### Column Description

| Column         | Description                         |
| -------------- | ----------------------------------- |
| transaction_id | Unique ID for each transaction      |
| sale_date      | Date when the sale occurred         |
| sale_time      | Time of transaction                 |
| customer_id    | Unique customer identifier          |
| gender         | Gender of the customer              |
| age            | Age of the customer                 |
| category       | Product category                    |
| quantity       | Number of items purchased           |
| price_per_unit | Price of each item                  |
| cogs           | Cost of goods sold                  |
| total_sale     | Total sale value of the transaction |

---

# Data Cleaning

To ensure data reliability, records containing **NULL values** were identified and removed.

### Checking Missing Values

```sql
SELECT * FROM retail_sales
WHERE transaction_id IS NULL
OR sale_date IS NULL
OR sale_time IS NULL
OR customer_id IS NULL
OR gender IS NULL
OR age IS NULL
OR category IS NULL
OR quantity IS NULL
OR price_per_unit IS NULL
OR cogs IS NULL
OR total_sale IS NULL;
```

### Removing Invalid Records

```sql
DELETE FROM retail_sales
WHERE transaction_id IS NULL
OR sale_date IS NULL
OR sale_time IS NULL
OR customer_id IS NULL
OR gender IS NULL
OR age IS NULL
OR category IS NULL
OR quantity IS NULL
OR price_per_unit IS NULL
OR cogs IS NULL
OR total_sale IS NULL;
```

---

# Exploratory Data Analysis (EDA)

Basic queries were used to understand the dataset.

### Total Number of Sales

```sql
SELECT COUNT(*) FROM retail_sales;
```

### Total Number of Customers

```sql
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
```

### Product Categories

```sql
SELECT DISTINCT category FROM retail_sales;
```

---

# Business Questions & SQL Analysis

The following queries were written to extract meaningful insights from the dataset.

### 1. Sales on a Specific Date

```sql
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';
```

---

### 2. Clothing Sales with Quantity Greater Than 4 (Nov 2022)

```sql
SELECT *
FROM retail_sales
WHERE category = 'Clothing'
AND quantity >= 4
AND TO_CHAR(sale_date,'YYYY-MM') = '2022-11';
```

---

### 3. Total Sales by Category

```sql
SELECT
category,
SUM(total_sale) AS total_sales,
COUNT(*) AS total_orders
FROM retail_sales
GROUP BY category;
```

---

### 4. Average Age of Customers Purchasing Beauty Products

```sql
SELECT ROUND(AVG(age),2) AS average_age
FROM retail_sales
WHERE category = 'Beauty';
```

---

### 5. Transactions with Sales Greater Than 1000

```sql
SELECT *
FROM retail_sales
WHERE total_sale > 1000
ORDER BY total_sale;
```

---

### 6. Transactions by Gender and Category

```sql
SELECT
category,
gender,
COUNT(*) AS total_transactions
FROM retail_sales
GROUP BY category, gender;
```

---

### 7. Best Selling Month Each Year

```sql
SELECT year, month, avg_sales
FROM
(
SELECT
EXTRACT(YEAR FROM sale_date) AS year,
EXTRACT(MONTH FROM sale_date) AS month,
AVG(total_sale) AS avg_sales,
RANK() OVER(
PARTITION BY EXTRACT(YEAR FROM sale_date)
ORDER BY AVG(total_sale) DESC
) AS rank
FROM retail_sales
GROUP BY 1,2
) t
WHERE rank = 1;
```

---

### 8. Top 5 Customers by Total Sales

```sql
SELECT
customer_id,
SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;
```

---

### 9. Unique Customers per Category

```sql
SELECT
category,
COUNT(DISTINCT customer_id) AS unique_customers
FROM retail_sales
GROUP BY category;
```

---

### 10. Sales by Time Shift

```sql
WITH hourly_sales AS
(
SELECT *,
CASE
WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
ELSE 'Evening'
END AS shift
FROM retail_sales
)

SELECT
shift,
COUNT(*) AS total_orders
FROM hourly_sales
GROUP BY shift;
```

---

# Key Insights

* Retail transactions include multiple product categories such as **Clothing and Beauty**.
* Several purchases exceed **1000 in total sale value**, indicating high-value transactions.
* Sales vary across months, helping identify **high-performing periods**.
* Certain customers contribute significantly to total revenue.

---

# Conclusion

This project demonstrates how SQL can be used to perform **data cleaning, exploratory data analysis, and business intelligence**. By analyzing retail sales data, we can identify customer trends, category performance, and sales patterns that support data-driven decision making.

---

# How to Use This Project

1. Clone this repository
2. Create the database and table
3. Import the dataset
4. Run the SQL queries to reproduce the analysis
5. Modify queries to explore additional insights

---

# Author

**Muhammad Hassan**

If you want, I can also help you make this **10× more professional like a real Data Analyst portfolio project (with badges, folder structure, dataset section, screenshots, etc.)**, which will make your GitHub stand out.
