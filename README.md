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
