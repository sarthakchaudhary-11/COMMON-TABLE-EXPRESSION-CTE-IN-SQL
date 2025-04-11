📊 Sales Data Analysis Using CTEs (MySQL)
This project demonstrates how to use Common Table Expressions (CTEs) in MySQL to analyze sales data efficiently. It includes sample data, table creation, and multiple query examples using both basic and advanced CTEs.

🗂️ Table: sales
This table stores monthly revenue data for sales employees across different regions.

Columns:
Column Name	Data Type	Description
sale_id	INT (PK)	Auto-incremented sale ID
employee_name	VARCHAR(100)	Name of the employee
region	VARCHAR(50)	Region of sales
month	VARCHAR(20)	Month of the sales record
revenue	INT	Revenue generated in that month
📥 Sample Data
Example entries:

sql
Copy
Edit
('Amit', 'North', 'January', 5000),
('Amit', 'North', 'February', 6000),
('Riya', 'South', 'January', 4000),
('Raj',  'North', 'February', 5200),
...
🔍 CTE Queries
✅ 1. Total Revenue per Employee
sql
Copy
Edit
WITH employee_revenue AS (
    SELECT employee_name, SUM(revenue) AS total_revenue
    FROM sales
    GROUP BY employee_name
)
SELECT *
FROM employee_revenue
ORDER BY total_revenue DESC;
✅ 2. Top Performer per Region
sql
Copy
Edit
WITH ranked_sales AS (
    SELECT 
        employee_name, region, SUM(revenue) AS total_revenue,
        RANK() OVER (PARTITION BY region ORDER BY SUM(revenue) DESC) AS rank_in_region
    FROM sales
    GROUP BY employee_name, region
)
SELECT *
FROM ranked_sales
WHERE rank_in_region = 1;
✅ 3. Compare Employee Revenue to Monthly Average
sql
Copy
Edit
WITH monthly_avg AS (
    SELECT month, AVG(revenue) AS avg_revenue
    FROM sales
    GROUP BY month
)
SELECT s.employee_name, s.month, s.revenue, m.avg_revenue
FROM sales s
JOIN monthly_avg m ON s.month = m.month
WHERE s.revenue > m.avg_revenue;
📘 Learning Objectives
Understand and implement Common Table Expressions (CTEs).

Use window functions like RANK() with CTEs.

Improve query readability and avoid subquery repetition.

Perform comparative and aggregated analysis easily.

