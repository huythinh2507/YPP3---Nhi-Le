# A. Customer Nodes Exploration
## 1. How many unique nodes are there on the Data Bank system?
```sql
SELECT COUNT(DISTINCT node_id) AS unique_nodes
FROM data_bank.customer_nodes
```
## 2. What is the number of nodes per region?
```sql
SELECT 
	r.region_id, 
	r.region_name,
	COUNT(DISTINCT cn.node_id) AS count_nodes
FROM data_bank.customer_nodes AS cn
	JOIN data_bank.regions AS r
	ON r.region_id = cn.region_id
GROUP BY r.region_id, r.region_name
ORDER BY region_id
```
## 3. How many customers are allocated to each region?
```sql
SELECT 
	r.region_id, 
	r.region_name,
	COUNT(cn.customer_id) AS count_customer 
FROM data_bank.customer_nodes AS cn
	JOIN data_bank.regions AS r
	ON r.region_id = cn.region_id
GROUP BY r.region_id, r.region_name
ORDER BY region_id
```
## 4. How many days on average are customers reallocated to a different node?
WITH node_days AS (
	SELECT 
	customer_id,
	node_id,
	SUM(end_date - start_date) AS node_days
	FROM data_bank.customer_nodes
	WHERE end_date != '9999-12-31'
	GROUP BY customer_id, node_id
	ORDER BY customer_id, node_id
)
	
SELECT ROUND(AVG(node_days), 0) AS avg_reallocated_days
FROM node_days
--This is calculating for AVG DATE which customers reallocate to A DIFFERENT NODE

## 5. What is the median, 80th and 95th percentile for this same reallocation days metric for each region?
```sql
```


# B. Customer Transactions
## 1. What is the unique count and total amount for each transaction type?
```sql
SELECT 
	txn_type,
	COUNT(customer_id) AS count_transaction,
	SUM(txn_amount) AS sum_txt_amount
FROM data_bank.customer_transactions
GROUP BY txn_type
ORDER BY txn_type
```

## 2. What is the average total historical deposit counts and amounts for all customers?
```sql
WITH deposit_transactions AS (
	SELECT 
		customer_id,
		txn_type,
		COUNT(customer_id) AS count_transactions,
		AVG(txn_amount) AS avg_txt_amount
	FROM data_bank.customer_transactions
	WHERE txn_type = 'deposit'
	GROUP BY customer_id, txn_type
	ORDER BY customer_id
)

SELECT 
	ROUND(AVG(count_transactions),0) AS avg_deposit_transaction,
	ROUND(AVG(avg_txt_amount),0) AS avg_deposit_txt_amount
FROM deposit_transactions
```

## 3. For each month - how many Data Bank customers make more than 1 deposit and either 1 purchase or 1 withdrawal in a single month? (X)
```sql 
-- Author is wrong at CASE WHEN ... THEN 
WITH monthly_transactions AS (
	SELECT 
	customer_id,
	EXTRACT(month from txn_date) AS month,
	SUM(CASE WHEN txn_type = 'deposit' THEN 1 else 0 END) AS count_deposit, 
	SUM(CASE WHEN txn_type = 'purchase' THEN 1 else 0 END) AS count_purchase,
	SUM(CASE WHEN txn_type = 'withdrawal' THEN 1 else 0 END) AS count_withdrawal
FROM data_bank.customer_transactions
GROUP BY customer_id, month
ORDER BY customer_id
)

SELECT month, count(customer_id)
FROM monthly_transactions
WHERE count_deposit > 1 
	AND (count_purchase > 0 OR count_withdrawal > 0)
GROUP BY month
ORDER BY month
```
WITH sum_amount AS (
	SELECT 
	customer_id,
	EXTRACT(month from txn_date) AS month,
	SUM(CASE WHEN txn_type = 'deposit' THEN txn_amount ELSE 0 END) AS sum_deposit,
	SUM(CASE WHEN txn_type = 'purchase' THEN txn_amount ELSE 0 END) AS sum_purchase,
	SUM(CASE WHEN txn_type = 'withdrawal' THEN txn_amount ELSE 0 END) AS sum_withdrawal
FROM data_bank.customer_transactions
GROUP BY customer_id, month
ORDER BY customer_id, month
)

SELECT customer_id, month, (sum_deposit - sum_purchase - sum_withdrawal) AS closing_balance
FROM sum_amount

