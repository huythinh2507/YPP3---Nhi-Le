## 0. Clean data and transform
```sql
-- Table 1: pizza_runner.customer_orders
CREATE TEMP TABLE customer_orders_temp AS 
SELECT 
  order_id, 
  customer_id, 
  pizza_id, 
  CASE
	  WHEN exclusions IS null OR exclusions LIKE 'null' OR exclusions = '' THEN NULL
	  ELSE exclusions
	  END AS exclusions,
  CASE
	  WHEN extras IS NULL or extras LIKE 'null' OR extras = '' THEN NULL
	  ELSE extras
	  END AS extras,
	order_time
FROM pizza_runner.customer_orders;
```

```sql
-- Table 2: pizza_runner.
CREATE TEMP TABLE runner_orders_temp AS
	SELECT 
	order_id, 
	runner_id, 
	CASE
		WHEN pickup_time IS NULL OR pickup_time LIKE 'null' THEN NULL
		ELSE pickup_time :: TIMESTAMP
		END AS pickup_time,
	CASE 
		WHEN distance IS NULL OR distance LIKE 'null' THEN NULL
		WHEN distance LIKE '%km' THEN TRIM('%km' FROM distance)::FLOAT
		WHEN distance LIKE '% km' THEN TRIM('% km' FROM distance)::FLOAT
		ELSE distance::FLOAT
		END AS distance,
	CASE 
		WHEN duration IS NULL OR duration LIKE 'null' THEN NULL 
		WHEN duration LIKE '%minutes' THEN TRIM('%minutes' FROM duration)::INT
		WHEN duration LIKE ' %minute' THEN TRIM(' %minute' FROM duration)::INT
		WHEN duration LIKE '%mins' THEN TRIM('%mins' FROM duration)::INT
		WHEN duration LIKE '% mins' THEN TRIM('% mins' FROM duration)::INT
		WHEN duration LIKE '% minute' THEN TRIM('% minute' FROM duration)::INT
		WHEN duration LIKE '%minute' THEN TRIM('%minute' FROM duration)::INT
		ELSE duration::INT
		END AS duration,
	CASE 
		WHEN cancellation  LIKE 'null' OR cancellation = '' THEN NULL
		ELSE cancellation
		END AS cancellation
FROM pizza_runner.runner_orders
```

# A. Pizza Metrics
## 1. How many pizzas were ordered?
```sql
SELECT COUNT(order_id) AS count_pizza_order
FROM customer_orders_temp
```

## 2. How many unique customer orders were made?
```sql
SELECT COUNT(distinct order_id) AS count_unique_order
FROM customer_orders_temp
```

## 3. How many successful orders were delivered by each runner?
```sql
SELECT runner_id, COUNT(order_id) AS count_successful_order
FROM runner_orders_temp 
WHERE distance !=0
GROUP BY runner_id
ORDER BY runner_id
```

## 4. How many of each type of pizza was delivered?
```sql
SELECT pn.pizza_name, COUNT(c.pizza_id) AS count_pizza_delivered
FROM runner_orders_temp AS r
	JOIN customer_orders_temp AS c 
	ON r.order_id = c.order_id
	JOIN pizza_runner.pizza_names AS pn
	ON c.pizza_id = pn.pizza_id
WHERE distance !=0
GROUP BY pn.pizza_name
```

## 5. How many Vegetarian and Meatlovers were ordered by each customer?**
```sql
SELECT c.customer_id, pn.pizza_name, COUNT(c.order_id) AS count_order
FROM pizza_runner.pizza_names AS pn
JOIN customer_orders_temp AS c
ON pn.pizza_id = c.pizza_id
GROUP BY c.customer_id, pn.pizza_name
ORDER BY c.customer_id
```

## 6. What was the maximum number of pizzas delivered in a single order?
```sql
WITH pizza_per_order_cte AS (
SELECT order_id, COUNT(pizza_id) AS count_pizza
FROM customer_orders_temp
GROUP BY order_id
ORDER BY order_id
)
SELECT MAX(count_pizza) as max_pizza
FROM pizza_per_order_cte
```

## 7. For each customer, how many delivered pizzas had at least 1 change and how many had no changes?
```sql
```
## 8. How many pizzas were delivered that had both exclusions and extras?
```sql
```
## 9. What was the total volume of pizzas ordered for each hour of the day?
```sql
---Method 1:
SELECT 
   DATE_PART('hour', order_time) AS hour_of_day, 
   COUNT(order_id) AS total_volume_pizza
FROM customer_orders_temp
GROUP BY hour_of_day
ORDER BY hour_of_day
```

```sql
---Method 2:
SELECT 
   EXTRACT(HOUR FROM order_time) AS hour_of_day, 
   COUNT(order_id) AS total_pizza
FROM customer_orders_temp
GROUP BY EXTRACT(HOUR FROM order_time) 
ORDER BY EXTRACT(HOUR FROM order_time) 
```

## 10. What was the volume of orders for each day of the week?
```sql
SELECT EXTRACT(DOW FROM order_time) AS day_of_week, COUNT(order_id) AS count_pizza
FROM customer_orders_temp
GROUP BY day_of_week
ORDER BY day_of_week 
```

# B. Runner and Customer Experience
## 1. How many runners signed up for each 1 week period? (i.e. week starts 2021-01-01)
```sql
SELECT 
   DATE_PART('week', registration_date) AS registration_week, 
   COUNT(runner_id) AS count_runner
FROM pizza_runner.runners
GROUP BY registration_week
```

## 2. What was the average time in minutes it took for each runner to arrive at the Pizza Runner HQ to pickup the order?
```sql
SELECT AVG(DATE_PART('minute', r.pickup_time - c.order_time)) AS avg_pickup_time
FROM customer_orders_temp AS c
JOIN runner_orders_temp AS r
ON c.order_id = r.order_id
```

## 3.  Is there any relationship between the number of pizzas and how long the order takes to prepare?
```sql
WITH time_prepare_cte AS (
SELECT 
	c.order_id, 
	COUNT(c.order_id) AS count_pizza ,
	DATE_PART('minute', r.pickup_time - c.order_time) AS datediff
FROM customer_orders_temp AS c
JOIN runner_orders_temp AS r
ON c.order_id = r.order_id
WHERE r.distance != 0
GROUP BY c.order_id, datediff
ORDER BY c.order_id
)

SELECT 
	count_pizza, 
	AVG(datediff) AS Avg_time_prepare
FROM time_prepare_cte
GROUP BY count_pizza
ORDER BY count_pizza
```

## 4. What was the average distance travelled for each customer?
```sql
SELECT 
	c.customer_id, 
	ROUND(AVG(r.duration),2) AS Avg_travel_diration
FROM runner_orders_temp AS r
JOIN customer_orders_temp AS c
	ON c.order_id = r.order_id
WHERE duration IS NOT NULL
GROUP BY c.customer_id
ORDER BY c.customer_id
```

## 5. What was the difference between the longest and shortest delivery times for all orders?
```sql
SELECT 
	MAX(duration) AS max_duration, 
	MIN(duration) AS min_duration,
	MAX(duration) - MIN(duration) AS different_duration
FROM runner_orders_temp
```

## 6. What was the average speed for each runner for each delivery and do you notice any trend for these values?
```sql
```
## 7. What is the successful delivery percentage for each runner?
```sql
```



