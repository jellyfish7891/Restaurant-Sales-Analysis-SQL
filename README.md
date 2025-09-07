# Restaurant-Sales-Analysis-SQL

SQL project analyzing restaurant sales data with joins, aggregates, and case logic to uncover key business trends.

## Tools Used
- MySQL  

## Goal
Query and analyze restaurant sales and store data to identify revenue drivers, uncover patterns, and support management decision-making.  

## Process
- Queried large transactional datasets using `JOIN`, `CASE`, and `GROUP BY`.  
- Aggregated sales metrics (revenue, top products, regional performance).  
- Analyzed sales variation by product, country, and payment method.  
- Built logic to flag anomalies (e.g., theft amounts above a threshold).  

## Key Queries & Examples

```sql
-- Total revenue
SELECT ROUND(SUM(price * quantity_sold), 2) AS revenue
FROM sales;

-- Best-selling products by total quantity sold
SELECT product_name,
       SUM(quantity_sold) AS total_sold
FROM sales
GROUP BY product_name
ORDER BY total_sold DESC;

-- Country with the most sales
SELECT country,
       SUM(quantity_sold) AS total_quantity_sold
FROM sales 
INNER JOIN store
       ON sales.storeid = store.storeid
GROUP BY country
ORDER BY total_quantity_sold DESC;

-- Managers with theft amounts > 100
SELECT general_manager,
       age,
       amounts,
       CASE
           WHEN amounts > 100 THEN 'send email'
           ELSE 'no action'
       END AS next_steps
FROM store
INNER JOIN theft
       ON store.storeid = theft.storeid;
```

**Outcome / Insights:**

Identified top-selling products and peak sales days.

Found that sales varied significantly by country and payment method.

Built automated logic to flag managers for further review when theft exceeded thresholds.

Provided actionable recommendations to support operational strategy and fraud monitoring.
