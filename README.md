# Retail-Sales-Analysis-SQL-Project
# Project Overview

**Project Title:** Retail Sales Analysis  
**Level:** Beginner  
**Database:** sql_project1

This project highlights foundational SQL skills applied to retail sales data. It encompasses database creation, data cleaning, exploratory analysis, and insights generation. Designed for aspiring data analysts, this project offers hands-on experience in analyzing sales data and addressing business queries using SQL.

# Objectives

**Database Creation:** Build and populate a structured database (sql_project1) to store retail sales records.  
**Data Cleaning:** Identify and handle records with missing or null values to ensure data quality.  
**Exploratory Data Analysis (EDA):** Conduct basic exploratory analyses to familiarize yourself with the dataset's structure and patterns.  
**Business Insights:** Utilize SQL queries to address specific business questions and extract actionable insights from the sales data.  

# Project Structure

**1. Database Setup**

- **Database Creation:** The project starts by creating a database named sql_project1.  
- **Table Creation:** A table named retail_sales is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.

### SQL Code

```sql
CREATE DATABASE p1_retail_db;

CREATE TABLE retail_sales
(
    transactions_id INT PRIMARY KEY,
    sale_date DATE,	
    sale_time TIME,
    customer_id INT,	
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,	
    cogs FLOAT,
    total_sale FLOAT
);
```
**2. Data Exploration & Cleaning**

- **Record Count:** Determine the total number of records in the dataset.
- **Customer Count:** Find out how many unique customers are in the dataset.
- **Category Count:** Identify all unique product categories in the dataset.
- **Null Value Check:** Check for any null values in the dataset and delete records with missing data.

### SQL Code

```sql
SELECT COUNT(*) FROM retail_sales;
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
SELECT DISTINCT category FROM retail_sales;

SELECT * FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;

DELETE FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;
```
**3. Data Analysis & Findings**
The following SQL queries were developed to answer specific business questions:

**1. Write a SQL query to retrieve all columns for sales made on '2022-11-05:**

### SQL Code

```sql
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';
```
**2. Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov-2022:**

### SQL Code
```sql
SELECT 
  *
FROM retail_sales
WHERE 
    category = 'Clothing'
    AND 
    TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
    AND
    quantity >= 4
```
**3. Write a SQL query to calculate the total sales (total_sale) for each category:**

### SQL Code
```sql
SELECT 
    category,
    SUM(total_sale) as net_sale,
    COUNT(*) as total_orders
FROM retail_sales
GROUP BY 1
```
**4. Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category:**

### SQL Code
```sql
SELECT
    ROUND(AVG(age), 2) as avg_age
FROM retail_sales
WHERE category = 'Beauty'
```
**5. Write a SQL query to find all transactions where the total_sale is greater than 1000:**

### SQL Code
```sql
SELECT * FROM retail_sales
WHERE total_sale > 1000
```

**6. Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category:**

### SQL Code
```sql
SELECT 
    category,
    gender,
    COUNT(*) as total_trans
FROM retail_sales
GROUP 
    BY 
    category,
    gender
ORDER BY 1
```
**7. Write a SQL query to calculate the average sale for each month. Find out best selling month in each year:**

### SQL Code
```sql
SELECT 
       year,
       month,
    avg_sale
FROM 
(    
SELECT 
    EXTRACT(YEAR FROM sale_date) as year,
    EXTRACT(MONTH FROM sale_date) as month,
    AVG(total_sale) as avg_sale,
    RANK() OVER(PARTITION BY EXTRACT(YEAR FROM sale_date) ORDER BY AVG(total_sale) DESC) as rank
FROM retail_sales
GROUP BY 1, 2
) as t1
WHERE rank = 1
```

**8. Write a SQL query to find the top 5 customers based on the highest total sales:**

### SQL Code
```sql
SELECT 
    customer_id,
    SUM(total_sale) as total_sales
FROM retail_sales
GROUP BY 1
ORDER BY 2 DESC
LIMIT 5
```

**9. Write a SQL query to find the number of unique customers who purchased items from each category:**

### SQL Code
```sql
SELECT 
    category,    
    COUNT(DISTINCT customer_id) as cnt_unique_cs
FROM retail_sales
GROUP BY category
```

**10. Write a SQL query to create each shift and number of orders (Example Morning <12, Afternoon Between 12 & 17, Evening >17):**

### SQL Code
```sql
WITH hourly_sale
AS
(
SELECT *,
    CASE
        WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
        WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening'
    END as shift
FROM retail_sales
)
SELECT 
    shift,
    COUNT(*) as total_orders    
FROM hourly_sale
GROUP BY shift
```
# Findings
- **Customer Demographics:** The data highlights diverse age groups among customers, with sales spanning categories like Clothing and Beauty.
- **Premium Transactions:** Several transactions exceed a total sale value of 1000, showcasing high-value purchases.
- **Seasonal Sales Patterns:** Monthly analysis reveals sales fluctuations, aiding in pinpointing peak sales periods.
- **Customer Behavior:** The study identifies top-spending customers and the most favored product categories.

# Reports
- **Sales Overview:** A comprehensive summary of total sales, customer demographics, and category-wise performance.
- **Trend Insights:** Analysis of monthly sales trends and peak activity shifts.
- **Customer Analysis:** Reports on high-value customers and unique buyer counts across product categories.

# Conclusion
This project provides a hands-on introduction to SQL for data analysis, covering database creation, data cleaning, and exploratory queries. The insights gained offer valuable perspectives on sales trends, customer preferences, and product success, forming a foundation for strategic business decisions.


