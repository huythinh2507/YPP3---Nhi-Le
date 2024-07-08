## Case Study #6: Clique Bait
- [Case Study #6: Clique Bait](https://8weeksqlchallenge.com/case-study-6/)
- [Reference Answer](https://github.com/katiehuangx/8-Week-SQL-Challenge/tree/main/Case%20Study%20%236%20-%20Clique%20Bait)

***

## 📚 My Solution
## A. Digital Analysis
### 1. How many users are there?
```sql
SELECT 
  COUNT(DISTINCT user_id) AS count_user
FROM clique_bait.users
```

### 2. How many cookies does each user have on average?
```sql
WITH cookies as (
SELECT 
	user_id,
	COUNT(cookie_id) AS count_cookies
FROM clique_bait.users
GROUP BY user_id
ORDER BY user_id
)

SELECT ROUND(AVG(count_cookies),0) AS avg_cookie_id
FROM cookies
```

### 3. What is the unique number of visits by all users per month?
```sql
SELECT 
	DATE_PART('MONTH', event_time) AS month,
	COUNT(DISTINCT visit_id) AS count_visit_id
FROM clique_bait.events
GROUP BY month
ORDER BY month
```

### 4. What is the number of events for each event type?
```sql
SELECT 
	event_type,
	COUNT(*) AS count_events
FROM clique_bait.events
GROUP BY event_type
ORDER BY event_type
```

### 5. What is the percentage of visits which have a purchase event?
```sql
1/
SELECT 
	ei.event_name,
	COUNT(distinct e.visit_id) AS count_visit_id,
	ROUND(100 * COUNT(distinct e.visit_id)::DECIMAL/(SELECT COUNT(distinct visit_id) FROM clique_bait.events),2) AS visit_percentage
FROM clique_bait.events AS e
	JOIN clique_bait.event_identifier AS ei
	ON e.event_type = ei.event_type
WHERE ei.event_name ILIKE 'purchase' -- remove WHERE to see visit percentage of each event_type
GROUP BY ei.event_name
ORDER BY ei.event_name
```

```sql
2/
WITH count_visit_purchase AS (
SELECT 
	ei.event_name, 
	COUNT(DISTINCT visit_id) AS count_visit
FROM clique_bait.events AS e
JOIN clique_bait.event_identifier AS ei
ON e.event_type = ei.event_type
WHERE ei.event_name ILIKE 'purchase'
GROUP BY ei.event_name
ORDER BY ei.event_name
)

SELECT ROUND(100 * count_visit/(SELECT COUNT(DISTINCT visit_id) FROM clique_bait.events),2) AS percentage_purchase
FROM count_visit_purchase
```

### 6. What is the percentage of visits which view the checkout page but do not have a purchase event?

### 7.  What are the top 3 pages by number of views?
```sql
SELECT ph.page_name, COUNT(e.page_id) AS count_view
FROM clique_bait.events AS e
JOIN clique_bait.page_hierarchy AS ph 
	ON e.page_id = ph.page_id
WHERE e.event_type = 1
GROUP BY ph.page_name
ORDER BY count_view desc
LIMIT 3
```

### 8. What is the number of views and cart adds for each product category?
```sql 
SELECT ph.product_category, 
	SUM(CASE WHEN e.event_type = 1 THEN 1 END) AS count_views, 
	SUM(CASE WHEN e.event_type = 2 THEN 1 END) AS count_cart_adds
FROM clique_bait.events AS e
JOIN clique_bait.page_hierarchy AS ph
	ON e.page_id = ph.page_id
WHERE product_category IS NOT NULL
GROUP BY ph.product_category
ORDER BY ph.product_category
```

### 9. What are the top 3 products by purchases?
```sql
SELECT ph.page_name, COUNT(e.page_id) AS count_purchases
FROM clique_bait.events AS e
	JOIN clique_bait.page_hierarchy AS ph
	ON e.page_id = ph.page_id
WHERE e.event_type = 3
GROUP BY ph.page_name
LIMIT 3
```
## B. Product Funnel Analysis
### 1. How many times was each product viewed?
### 2. How many times was each product added to cart?
### 3. How many times was each product added to a cart but not purchased (abandoned)?
### 4. How many times was each product purchased?

