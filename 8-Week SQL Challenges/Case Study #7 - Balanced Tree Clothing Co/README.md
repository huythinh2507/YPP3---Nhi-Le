### A. High Level Sales Analysis
### 1. What was the total quantity sold for all products?
```sql
SELECT product_name, SUM(qty) AS sold_quantity
    FROM balanced_tree.sales AS s
    JOIN balanced_tree.product_details AS pd
    ON s.prod_id = pd.product_id
    GROUP BY product_name
		
	UNION 
	
    SELECT 'Total', SUM(qty) 
    FROM balanced_tree.sales
	ORDER BY sold_quantity 
```

### 2. What is the total generated revenue for all products before discounts?
```sql
SELECT pd.product_name, (s.qty * s.price) AS revenue
FROM balanced_tree.sales AS s
JOIN balanced_tree.product_details AS pd
ON s.prod_id = pd.product_id
	
UNION
	
SELECT 'Total' as prod_id, SUM(qty * price)
FROM balanced_tree.sales
ORDER BY revenue DESC
```
### 3. What was the total discount amount for all products?
```sql
SELECT SUM(qty * price * discount/100) AS Total_discount
FROM balanced_tree.sales
```

## B. Transaction Analysis
### 1. How many unique transactions were there?
```sql
SELECT COUNT(DISTINCT txn_id) AS txn_count
FROM balanced_tree.sales
```

### 2. What is the average unique products purchased in each transaction?
```sql
WITH count_product_id AS (
SELECT txn_id, count(prod_id) AS count_product
FROM balanced_tree.sales
group by txn_id
order by txn_id
)

SELECT ROUND(AVG(count_product)) AS avg_product_id
FROM count_product_id
```

### 3. What are the 25th, 50th and 75th percentile values for the revenue per transaction?
```sql
with revenue as (
	select txn_id, SUM((qty * price) - (qty * price * discount/100)) as revenue 
	from balanced_tree.sales
	group by txn_id
)
	
SELECT
percentile_cont(0.25) within group (order by revenue) as percentile_25th,
percentile_cont(0.5) within group (order by revenue) as percentile_50th,
percentile_cont(0.75) within group (order by revenue) as percentile_75th
FROM revenue
```

### 4. What is the average discount value per transaction?
```sql 
WITH txn_discount AS (
SELECT txn_id, SUM(qty * price * discount/100) as discount_value
FROM balanced_tree.sales
GROUP BY txn_id
order by txn_id
)

SELECT ROUND(AVG(discount_value)) AS avg_discount
FROM txn_discount
```

### 5. What is the percentage split of all transactions for members vs non-members?
```sql WITH CTE AS (
SELECT 
	member, 
	count(DISTINCT txn_id) AS count_txn
FROM balanced_tree.sales
GROUP BY member
ORDER BY member
)

SELECT 
	member, 
	ROUND(100 * count_txn/(SELECT SUM(count_txn) FROM CTE)) AS percentage
FROM CTE
```

### 6. What is the average revenue for member transactions and non-member transactions?
```sql
WITH member_revenue AS (
SELECT member, txn_id, SUM((qty * price) - (qty * price * discount/100)) AS revenue
FROM balanced_tree.sales
GROUP BY member, txn_id
ORDER BY member, txn_id
)

SELECT member, ROUND(AVG(revenue)) AS avg_member_revenue
FROM member_revenue
GROUP BY member
ORDER BY member
```

## C. Product Analysis
### 1. What are the top 3 products by total revenue before discount?
```sql 
SELECT 
	s.prod_id, 
	pd.product_name,
	SUM(s.qty * s.price) AS revenue_bef_disc
FROM balanced_tree.sales AS s
	JOIN balanced_tree.product_details AS pd
	ON s.prod_id = pd.product_id
GROUP BY s.prod_id, pd.product_name
ORDER BY revenue_bef_disc DESC
LIMIT 3
```

### 2. What is the total quantity, revenue and discount for each segment?
```sql
SELECT 
	pd.segment_name, 
	COUNT(s.qty) AS count_qty,
	SUM(s.qty * s.price - s.qty * s.price * discount/100) AS total_revenue,
	SUM(s.qty * s.price * discount/100) AS total_discount
FROM balanced_tree.product_details AS pd
JOIN balanced_tree.sales AS s
ON pd.product_id = s.prod_id
GROUP BY pd.segment_name
ORDER BY pd.segment_name
```

### 3. What is the top selling product for each segment?
```sql
WITH rank_segment AS (
SELECT 
	pd.segment_id,
	pd.segment_name,
	pd.product_id,
	pd.product_name,
	SUM(s.qty) AS total_quantity,
	RANK() OVER(PARTITION BY pd.segment_name ORDER BY SUM(s.qty) DESC) AS rank 
FROM balanced_tree.product_details AS pd
JOIN balanced_tree.sales AS s
ON pd.product_id = s.prod_id
GROUP BY segment_id, segment_name, pd.product_id, pd.product_name
)

SELECT 
	segment_name, product_name, total_quantity
FROM rank_segment
WHERE rank = 1
```

### 4. What is the total quantity, revenue and discount for each category?
```sql
SELECT 
	pd.category_name,
	SUM(s.qty) AS total_quantity,
	SUM(s.qty * s.price - s.qty * s.price * s.discount/100) AS total_revenue,
	SUM(s.qty * s.price * s.discount/100) AS total_discount
FROM balanced_tree.product_details AS pd
JOIN balanced_tree.sales AS s
ON pd.product_id = s.prod_id
GROUP BY pd.category_name
```

### 5. What is the top selling product for each category?
```sql
WITH rank_category AS (
SELECT 
	pd.category_id,
	pd.category_name,
	pd.product_id,
	pd.product_name,
	SUM(s.qty) AS total_quantity,
	RANK() OVER(PARTITION BY pd.category_id ORDER BY SUM(s.qty) DESC) AS rank
FROM balanced_tree.product_details AS pd
JOIN balanced_tree.sales AS s
ON pd.product_id = s.prod_id
GROUP BY pd.category_id, pd.category_name, pd.product_id, pd.product_name
)

SELECT category_name, product_name, total_quantity
FROM rank_category
WHERE rank = 1
ORDER BY category_name
```

### 6. What is the percentage split of revenue by product for each segment?
```sql
WITH product_revenue AS (
SELECT 
	pd.segment_name,
	pd.product_name,
	SUM(s.qty * s.price - s.qty * s.price * s.discount/100) AS total_revenue 
FROM balanced_tree.product_details AS pd
JOIN balanced_tree.sales AS s
	ON pd.product_id = s.prod_id
GROUP BY pd.segment_name, pd.product_name
)

SELECT 
	segment_name, product_name,
	ROUND(100 * total_revenue/(SELECT SUM(total_revenue) FROM segment_revenue),1) AS percentage
FROM product_revenue
ORDER BY segment_name
```

### 7. What is the percentage split of revenue by segment for each category?
```sql
WITH segment_revenue AS (
SELECT 
	pd.segment_id,
	pd.segment_name,
	pd.category_id,
	pd.category_name,
	SUM(s.qty * s.price - s.qty * s.price * s.discount/100) AS total_revenue 
FROM balanced_tree.product_details AS pd
JOIN balanced_tree.sales AS s
	ON pd.product_id = s.prod_id
GROUP BY pd.segment_id, pd.segment_name, pd.category_id, pd.category_name
)

SELECT 
	category_name, segment_name,
	ROUND(100 * total_revenue/(SELECT SUM(total_revenue) FROM segment_revenue),1) AS percentage
FROM segment_revenue
ORDER BY category_name, percentage
```

### 8. What is the percentage split of total revenue by category?
```sql
WITH segment_revenue AS (
SELECT 
	pd.category_id,
	pd.category_name,
	SUM(s.qty * s.price - s.qty * s.price * s.discount/100) AS total_revenue 
FROM balanced_tree.product_details AS pd
JOIN balanced_tree.sales AS s
	ON pd.product_id = s.prod_id
GROUP BY pd.category_id, pd.category_name
)

SELECT 
	category_name,
	ROUND(100 * total_revenue/(SELECT SUM(total_revenue) FROM segment_revenue),1) AS percentage
FROM segment_revenue
ORDER BY category_name, percentage
```

### 9. What is the total transaction “penetration” for each product? (hint: penetration = number of transactions where at least 1 quantity of a product was purchased divided by total number of transactions)
```sql 
WITH count_txn AS(
	SELECT 
	s.prod_id, 
	pd.product_name,
	count(s.txn_id) AS count_txn 
FROM balanced_tree.sales AS s
	JOIN balanced_tree.product_details AS pd
	ON s.prod_id = pd.product_id
GROUP BY s.prod_id, pd.product_name
ORDER BY s.prod_id
)

SELECT 
	product_name,
	ROUND(100.0 * count_txn/(SELECT SUM(count_txn) FROM count_txn),2) AS penetration		
FROM count_txn
```

### 10. What is the most common combination of at least 1 quantity of any 3 products in a 1 single transaction?
```sql
WITH CTE AS (
SELECT s.txn_id, s.prod_id, pd.product_name
FROM balanced_tree.sales AS s
	JOIN balanced_tree.product_details AS pd
	ON s.prod_id = pd.product_id
)
SELECT  
	c1.product_name, 
	c2.product_name, 
	c3.product_name, 
	COUNT(*) AS count_frequency
FROM CTE AS c1
INNER JOIN CTE AS c2
ON c1.txn_id = c2.txn_id
INNER JOIN CTE AS c3
ON c1.txn_id = c3.txn_id
WHERE c1.prod_id > c2.prod_id AND c2.prod_id > c3.prod_id
GROUP BY c1.product_name, c2.product_name,  c3.product_name
ORDER BY c1.product_name, c2.product_name,  c3.product_name
```