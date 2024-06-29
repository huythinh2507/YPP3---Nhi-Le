## Case Study #1 - Danny's Diner
- [Case Study #1 - Danny's Diner ](https://8weeksqlchallenge.com/case-study-1/)
- [Reference Answer](https://8weeksqlchallenge.com/case-study-1/)

## My Solution
## 1. What is the total amount each customer spent at the restaurant?
```sql
SELECT 
  sales.customer_id, 
  SUM(menu.price) AS Total
FROM dannys_diner.sales 
JOIN dannys_diner.menu
  ON sales.product_id = menu.product_id
GROUP BY sales.customer_id
ORDER BY sales.customer_id
```

## 2. How many days has each customer visited the restaurant?
```sql
SELECT 
  customer_id, 
  COUNT(distinct order_date)
FROM dannys_diner.sales
GROUP BY customer_id
ORDER BY customer_id
```

## 3. What was the first item from the menu purchased by each customer?
```sql
WITH sales_order_cte AS (
SELECT 
  sales.customer_id, 
  sales.order_date, 
  menu.product_name,
  DENSE_RANK() OVER (PARTITION BY sales.customer_id ORDER BY sales.order_date) AS rank
FROM dannys_diner.sales 
JOIN dannys_diner.menu
  ON sales.product_id = menu.product_id
)
SELECT 
  customer_id, 
  product_name
FROM sales_order_cte
WHERE rank = 1
GROUP BY customer_id, product_name
ORDER BY customer_id
```

## 4. What is the most purchased item on the menu and how many times was it purchased by all customers?
```sql
SELECT 
  menu.product_name, 
  COUNT(sales.product_id) AS total_times
FROM dannys_diner.sales
JOIN dannys_diner.menu
  ON menu.product_id = sales.product_id
GROUP BY menu.product_name
ORDER BY total_times DESC
LIMIT 1
```

## 5. Which item was the most popular for each customer?
```sql
WITH count_order_cte AS (
SELECT 
  sales.customer_id, menu.product_name, 	
  COUNT(menu.product_id) AS total_times, 
  DENSE_RANK() OVER (PARTITION BY sales.customer_id ORDER BY COUNT(sales.product_id) DESC) AS rank 
FROM dannys_diner.menu
JOIN dannys_diner.sales 
  ON sales.product_id = menu.product_id
GROUP BY sales.customer_id, menu.product_name
)
SELECT 
  customer_id, 
  product_name, 
  total_times
FROM count_order_cte
WHERE rank = 1
```

## 6. Which item was purchased first by the customer after they became a member?
```sql
--Xài DENSE_RANK()
WITH order_after_member_cte AS(
SELECT 
  sales.customer_id, 
  menu.product_name, 
  DENSE_RANK() OVER (PARTITION BY sales.customer_id ORDER BY sales.order_date ASC) AS rank
FROM dannys_diner.members
JOIN dannys_diner.sales 
  ON members.customer_id = sales.customer_id
JOIN dannys_diner.menu
  ON sales.product_id = menu.product_id
WHERE members.join_date < sales.order_date
GROUP BY sales.customer_id, menu.product_name, sales.order_date
ORDER BY sales.customer_id
)

SELECT 
  customer_id, 
  product_name
FROM order_after_member_cte
WHERE rank = 1
```
```sql
--C2: Giống tác giả, xài DENSE_RANK()
WITH order_after_member_cte AS (
SELECT 
  sales.customer_id, 
  sales.product_id, 
  DENSE_RANK() OVER (PARTITION BY sales.customer_id ORDER BY sales.order_date ASC) AS rank
FROM dannys_diner.members
JOIN dannys_diner.sales 
  ON members.customer_id = sales.customer_id
WHERE members.join_date < sales.order_date
GROUP BY sales.customer_id, sales.product_id, sales.order_date
ORDER BY sales.customer_id
)
SELECT 
  order_after_member_cte.customer_id, 
  menu.product_name
FROM order_after_member_cte
JOIN dannys_diner.menu
  ON order_after_member_cte.product_id = menu.product_id
WHERE rank = 1
ORDER BY order_after_member_cte.customer_id
``` 

## 7. Which item was purchased just before the customer became a member?
```sql
-- Tác giả làm sai, dùng NUM_ROW() để rank đã bỏ qua orders cùng ngày order
WITH order_before_member_cte AS (
SELECT sales.customer_id, menu.product_name, sales.order_date, DENSE_RANK() OVER (PARTITION BY sales.customer_id ORDER BY sales.order_date DESC) AS rank
FROM dannys_diner.sales 
JOIN dannys_diner.members
  ON sales.customer_id = members.customer_id
JOIN dannys_diner.menu
  ON sales.product_id = menu.product_id
WHERE sales.order_date < members.join_date 
ORDER BY sales.customer_id
)
SELECT 
  customer_id, 
  product_name
FROM order_before_member_cte
WHERE rank = 1
```

## 8. What is the total items and amount spent for each member before they became a member?
```sql
SELECT 
  sales.customer_id, 
  COUNT(sales.product_id) AS total_items, 
  SUM (menu.price)
FROM dannys_diner.sales
JOIN dannys_diner.members
  ON sales.customer_id = members.customer_id 
  AND members.join_date > sales.order_date -- can use WHERE (below) instead AND
JOIN dannys_diner.menu
  ON sales.product_id = menu.product_id
--WHERE members.join_date > sales.order_date (instead of AND above)
GROUP BY sales.customer_id
ORDER BY sales.customer_id
```

## 9.  If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?
```sql
--Nếu point này tính cho tất cả khách hàng
WITH point_product_cte AS (
SELECT 
  menu.product_id,
  CASE 
  WHEN product_id = 1 THEN price * 20
  ELSE price * 10 END as points
FROM dannys_diner.menu
)
SELECT 
  sales.customer_id, 
  SUM(points) as total_point
FROM dannys_diner.sales 
JOIN point_product_cte 
  ON sales.product_id = point_product.product_id
GROUP BY sales.customer_id
ORDER BY sales.customer_id
```

```sql
--Nếu point này tính cho khách hàng SAU KHI trở thành thành viên
WITH point_product_cte AS (
SELECT 
  menu.product_id,
  CASE 
  WHEN product_id = 1 THEN price * 20
  ELSE price * 10 END as points
FROM dannys_diner.menu
)

SELECT 
  sales.customer_id, 
  sum(points) as points
FROM dannys_diner.sales
JOIN dannys_diner.members
  ON members.customer_id = sales.customer_id
  AND members.join_date < sales.order_date
JOIN point_product_cte 
  ON point_product_cte.product_id = sales.product_id
GROUP BY sales.customer_id
ORDER BY sales.customer_id
```

## 10. In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi - how many points do customer A and B have at the end of January?
```sql
WITH point_product_cte AS (
SELECT 
  menu.product_id,
  CASE 
  WHEN product_id = 1 THEN price * 20
  ELSE price * 10 END as points
FROM dannys_diner.menu
)

/* 
CASE 
WHEN [first 7-days] THEN SUM(points * 2)
ELSE SUM(points)
*/

SELECT 
  sales.customer_id
FROM dannys_diner.sales
JOIN dannys_diner.members
  ON sales.customer_id = members.customer_id 
```

