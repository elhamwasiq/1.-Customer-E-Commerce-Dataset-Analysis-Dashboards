-- 1: RFM(Recency, Frequency, Monetary) Analysis
SELECT customer_name, 
CURRENT_DATE - MAX(purchase_date) AS Recency,
COUNT(*) AS Frequency,
SUM(total_purchase_amount) AS Monetary,
CASE 
   WHEN CURRENT_DATE - MAX(purchase_date) <=30 THEN 5
   WHEN CURRENT_DATE - MAX(purchase_date) <=90 THEN 4
   ELSE 3
END AS R,
CASE 
   WHEN COUNT(*) <= 50 THEN 5
   WHEN COUNT(*) <=30 THEN 4
   ELSE 3
END AS F,
CASE 
   WHEN SUM(total_purchase_amount) <=100000 THEN 5
   WHEN SUM(total_purchase_amount) <=50000 THEN 4
   ELSE 3
END AS M
FROM f1
GROUP BY customer_name


-- 2: Changes in Total Revenue by Previous Month
SELECT EXTRACT(YEAR FROM purchase_date) AS yearly_sales,
TO_CHAR(SUM(total_purchase_amount), '999,999,999') AS current_year_sales,
TO_CHAR(LAG(SUM(total_purchase_amount), 1) OVER(ORDER BY EXTRACT(YEAR FROM purchase_date)), '999,999,999') AS Prev_year_Sales,
TO_CHAR((SUM(total_purchase_amount) - LAG(SUM(total_purchase_amount), 1) OVER(ORDER BY EXTRACT(YEAR FROM purchase_date))), '999,999,999') AS Revenue_Changes
FROM f1
GROUP BY EXTRACT(YEAR FROM purchase_date)
ORDER BY EXTRACT(YEAR FROM purchase_date)

-- 3: CLV(Customer Lifetime Value) Analysis
SELECT customer_name, 
SUM(total_purchase_amount)/COUNT(DISTINCT(purchase_date)) AS CLV
FROM f1
GROUP BY customer_name


-- 4: Total customers and Total purchases
SELECT COUNT(DISTINCT(customer_id)) AS Total_Customers, COUNT(customer_id) AS Total_Purchases from f1


-- 5: Yearly sales trend analysis
SELECT EXTRACT(YEAR FROM purchase_date), TO_CHAR(COUNT(*), '99,999') as Yearly_Sales_Count FROM f1
GROUP BY EXTRACT(YEAR FROM purchase_date)
ORDER BY EXTRACT(YEAR FROM purchase_date)


-- 6: Most popular products (top-selling items)
SELECT product_category, COUNT(*) AS total_count FROM f1
GROUP BY product_category 
ORDER BY total_count DESC

-- 7: Average purchase amount per customer
SELECT customer_name, ROUND(AVG(total_purchase_amount),0) FROM f1
GROUP BY customer_name


-- 8: Total revenue generated from sales
SELECT SUM(total_purchase_amount) AS total_revenue FROM f1




