# -Swiggy-Food-Delivery-SQL-Case-Study-MySQL-
![image](https://github.com/biswajit8167/-Swiggy-Food-Delivery-SQL-Case-Study-MySQL-/blob/15b9cfe0d760ae8f2b4524b666b909bd333de569/ChatGPT%20Image%20Jan%2017%2C%202026%2C%2011_18_43%20PM.png)
# 🍔 Food Delivery Data Analysis Project (SQL + Power BI)

## 📌 Project Overview

This project simulates a **real-world food delivery analytics case study (Swiggy / Zomato style)** where multiple operational datasets are analyzed to extract business insights, define KPIs, and support data-driven decision making.

As a **Data Analyst**, I used **SQL for data analysis and Power BI for visualization** to answer key business questions related to orders, customers, restaurants, riders, revenue, and delivery performance.

This project is designed to demonstrate **job-ready analytical skills** expected from a Data Analyst in real companies.

---

## 🎯 Business Problem Statement

Food delivery companies struggle with **high cancellation rates, delayed deliveries, low customer retention, and uneven restaurant performance**.

The goal of this analysis is to:

* Track core business KPIs
* Identify operational bottlenecks
* Analyze customer behavior and churn
* Evaluate restaurant and rider performance
* Provide insights to improve efficiency and revenue

---

## 🗂️ Dataset Description

The project uses **5 relational datasets**:

| Table       | Description                                                 |
| ----------- | ----------------------------------------------------------- |
| orders      | Order-level details including status, value, and timestamps |
| customers   | Customer demographics and registration data                 |
| restaurants | Restaurant details and location                             |
| riders      | Delivery partner information                                |
| deliveries  | Delivery times, rider mapping, and performance              |

---

## 🛠️ Tools & Technologies Used

* **SQL (Microsoft SQL server)** – Data extraction, joins, CTEs, window functions
* **Power BI** – Interactive dashboards & business reporting
* **Excel** – Data validation and exploration
* **GitHub** – Project versioning and portfolio showcase

---

## 🔍 Analysis Performed (SQL – 40 Business Queries)

### 1️⃣ Data Understanding & Quality Checks
**1.How many total records are there in each table (orders, customers, restaurants, riders, deliveries)?**
```sql
SELECT 'orders' AS table_name, COUNT(*) AS total_records FROM orders
UNION ALL
SELECT 'customers' AS table_name, COUNT(*) AS total_records FROM customers
UNION ALL
SELECT 'restaurants' AS table_name, COUNT(*) AS total_records FROM restaurants
UNION ALL
SELECT 'riders' AS table_name, COUNT(*) AS total_records FROM riders
UNION ALL
SELECT 'deliveries' AS table_name, COUNT(*) AS total_records FROM deliveries;
```
![image](https://github.com/biswajit8167/-Swiggy-Food-Delivery-SQL-Case-Study-MySQL-/blob/90d53e0858ac55636e7bf978827639ef4fd86a98/screenshot/Screenshot%20(157).png)

***2.What is the date range of orders in the dataset?***
```sql
SELECT 
    MIN(order_date) AS first_order_date,
    MAX(order_date) AS last_order_date,
    DATEDIFF(DAY, MIN(order_date), MAX(order_date)) AS total_days_covered
FROM orders;
```
![image](https://github.com/biswajit8167/-Swiggy-Food-Delivery-SQL-Case-Study-MySQL-/blob/8262a80626536d1dc79b5bdc6b6ac7c749ee1d35/screenshot/Screenshot%20(158).png)

***3.	Are there any duplicate order IDs in the orders table?***
```sql
SELECT 
    order_id,
    COUNT(*) AS duplicate_count
FROM orders
GROUP BY order_id
HAVING COUNT(*) > 1;
```
***There are no duplicates value in order table***


***4.Which columns contain NULL values and how many?***

***For orders***
```sql
SELECT 
    SUM(CASE WHEN order_id IS NULL THEN 1 ELSE 0 END) AS order_id_nulls,
    SUM(CASE WHEN customer_id IS NULL THEN 1 ELSE 0 END) AS customer_id_nulls,
    SUM(CASE WHEN restaurant_id IS NULL THEN 1 ELSE 0 END) AS restaurant_id_nulls,
    SUM(CASE WHEN order_date IS NULL THEN 1 ELSE 0 END) AS order_date_nulls,
    SUM(CASE WHEN order_status IS NULL THEN 1 ELSE 0 END) AS order_status_nulls,
    SUM(CASE WHEN total_amount IS NULL THEN 1 ELSE 0 END) AS total_amount_nulls,
    SUM(CASE WHEN rating IS NULL THEN 1 ELSE 0 END) AS rating_nulls
FROM orders;
```
![image](https://github.com/biswajit8167/-Swiggy-Food-Delivery-SQL-Case-Study-MySQL-/blob/7ca5c4a24501a9d858b0df93c61f39301ea22f9c/screenshot/Screenshot%20(159).png)

***For customers***
```sql
SELECT 
    SUM(CASE WHEN customer_id IS NULL THEN 1 ELSE 0 END) AS customer_id_nulls,
    SUM(CASE WHEN customer_name IS NULL THEN 1 ELSE 0 END) AS customer_name_nulls,
    SUM(CASE WHEN age IS NULL THEN 1 ELSE 0 END) AS age_nulls,
    SUM(CASE WHEN gender IS NULL THEN 1 ELSE 0 END) AS gender_nulls,
    SUM(CASE WHEN registration_date IS NULL THEN 1 ELSE 0 END) AS registration_nulls
FROM customers;
```
![image](https://github.com/biswajit8167/-Swiggy-Food-Delivery-SQL-Case-Study-MySQL-/blob/03c3eb1b666e627748ab9f8a86c77206570ee7cf/screenshot/Screenshot%20(160).png)

***For Restaurants***
```sql
SELECT 
    SUM(CASE WHEN restaurant_id IS NULL THEN 1 ELSE 0 END) AS restaurant_id_nulls,
    SUM(CASE WHEN restaurant_name IS NULL THEN 1 ELSE 0 END) AS restaurant_name_nulls,
    SUM(CASE WHEN city IS NULL THEN 1 ELSE 0 END) AS city_nulls,
     SUM(CASE WHEN opening_hours IS NULL THEN 1 ELSE 0 END) AS opening_hours_nulls
FROM restaurants;
```
![image](https://github.com/biswajit8167/-Swiggy-Food-Delivery-SQL-Case-Study-MySQL-/blob/c8c51fc4bedd91d603e3965372a23448b14feb0d/screenshot/Screenshot%20(161).png)

***For Deliveries***
```sql
SELECT 
    SUM(CASE WHEN delivery_id IS NULL THEN 1 ELSE 0 END) AS delivery_id_nulls,
    SUM(CASE WHEN order_id IS NULL THEN 1 ELSE 0 END) AS order_id_nulls,
    SUM(CASE WHEN delivery_status IS NULL THEN 1 ELSE 0 END) AS delivery_nulls,
    SUM(CASE WHEN delivery_time IS NULL THEN 1 ELSE 0 END) AS deliver_time_nulls,
    SUM(CASE WHEN rider_id IS NULL THEN 1 ELSE 0 END) AS rider_id_nulls
FROM deliveries;
```
### 2️⃣ Core Business KPIs

* Total orders & revenue
* Average Order Value (AOV)
* Daily & monthly revenue trends
* Repeat customer percentage
* New customer acquisition trend

### 3️⃣ Restaurant Performance Analysis

* Top & bottom restaurants by revenue
* Cancellation rate by restaurant
* Revenue contribution (Pareto analysis)
* Order trends by restaurant

### 4️⃣ Delivery & Rider Performance

* Average delivery time
* Late delivery rate
* Rider utilization & efficiency
* City-wise delivery performance

### 5️⃣ Customer Behavior & Retention

* Peak ordering hours
* Weekend vs weekday revenue
* Customer churn identification
* Customer segmentation (High/Medium/Low value)

### 6️⃣ Advanced Analytics (Resume-Strong)

* Window functions (RANK, DENSE_RANK)
* Running revenue totals
* Cohort retention analysis
* Pareto (80/20) customer analysis

---

## 📊 Power BI Dashboards

### 📈 Dashboard 1: Executive Overview

**Purpose:** Monitor overall business health

KPIs:

* Total Orders
* Total Revenue
* AOV
* Cancellation Rate
* Avg Delivery Time

Visuals:

* Revenue trend
* Orders by city
* Status breakdown
* Top restaurants

---

### 🚚 Dashboard 2: Operations & Delivery Performance

**Purpose:** Improve delivery efficiency

KPIs:

* Avg delivery time
* Late delivery %
* Orders per rider

Visuals:

* Rider performance ranking
* Delivery time by city
* Restaurant delays

---

### 👥 Dashboard 3: Customer & Restaurant Insights

**Purpose:** Growth & retention analysis

KPIs:

* Repeat customers %
* Revenue per customer
* Restaurant contribution %

Visuals:

* New vs returning customers
* Customer segmentation
* Top 20% revenue contributors

---

## 📁 Project Structure

```
Food-Delivery-Data-Analysis
│
├── SQL
│   ├── 01_data_exploration.sql
│   ├── 02_kpi_metrics.sql
│   ├── 03_business_insights.sql
│   └── 04_advanced_analysis.sql
│
├── PowerBI
│   ├── executive_dashboard.pbix
│   ├── operations_dashboard.pbix
│   └── customer_dashboard.pbix
│
├── Dataset
│
├── Insights
│   └── business_insights.pdf
│
└── README.md
```

---

## 📌 Key Business Insights

* 20% of restaurants generate nearly 75% of total revenue
* Late deliveries are concentrated in specific areas and restaurants
* Repeat customers contribute majority of revenue
* Delivery delays strongly impact cancellations
* Rider utilization varies significantly by city

---

## 💡 Recommendations

* Focus retention campaigns on high-value repeat customers
* Optimize rider allocation in high-delay zones
* Work with low-performing restaurants to reduce cancellations
* Introduce incentives for top-performing riders

---

## 👨‍💼 Why This Project Matters

This project demonstrates my ability to:

* Translate business problems into analytical questions
* Write complex, optimized SQL queries
* Build executive-ready dashboards
* Communicate insights clearly
* Think like a business analyst, not just a data person

---

## 📬 Contact

If you are a recruiter or hiring manager:

📧 Email: [biswajitmaity@example.com](mailto:biswajitmaity@example.com)
🔗 LinkedIn: [https://linkedin.com/in/your-profile](https://linkedin.com/in/your-profile)
💼 Portfolio: [https://github.com/your-username](https://github.com/your-username)

---

⭐ *If you found this project useful, please star the repository!*
