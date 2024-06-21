## 1. How many customers has Foodie-Fi ever had?
```sql
SELECT COUNT(DISTINCT customer_id) AS customer_number
FROM foodie_fi.subscriptions
```
## 2. What is the monthly distribution of trial plan start_date values for our dataset - use the start of the month as the group by value
```sql
SELECT DATE_PART('month', s.start_date) AS month_start, COUNT(s.customer_id)
FROM foodie_fi.subscriptions AS s
	JOIN foodie_fi.plans AS p
	ON s.plan_id = p.plan_id
WHERE p.plan_id = 0
GROUP BY DATE_PART('month', start_date)
ORDER BY month_start
```

##3. What plan start_date values occur after the year 2020 for our dataset? Show the breakdown by count of events for each plan_name.
```sql
SELECT p.plan_id, p.plan_name, COUNT(s.customer_id) count_customer
FROM foodie_fi.subscriptions AS s
	JOIN foodie_fi.plans AS p
	ON s.plan_id = p.plan_id
WHERE DATE_PART('year', start_date) > 2020
GROUP BY p.plan_id, p.plan_name
ORDER BY p.plan_id
```
##4. What is the customer count and percentage of customers who have churned rounded to 1 decimal place?
```sql
WITH count_customer_cte AS (
SELECT 
	COUNT(distinct s.customer_id) AS count_customer,
	SUM(CASE WHEN p.plan_id = 4 THEN 1 ELSE 0 END) AS churned_customer
FROM foodie_fi.subscriptions AS s
	JOIN foodie_fi.plans AS p
	ON s.plan_id = p.plan_id
)

SELECT 
	count_customer, 
	churned_customer,
	ROUND((churned_customer/count_customer::decimal) *100,1) AS percentage_churned_customer 
FROM count_customer_cte
```
##5. How many customers have churned straight after their initial free trial - what percentage is this rounded to the nearest whole number?
```sql
WITH ranked_cte AS (
SELECT 
	s.customer_id, 
	p.plan_id, 
	p.plan_name,
	ROW_NUMBER() OVER(PARTITION BY s.customer_id ORDER BY p.plan_id) AS order_plan
FROM foodie_fi.subscriptions AS s
JOIN foodie_fi.plans AS p
ON p.plan_id = s.plan_id
)

SELECT 
	(SELECT COUNT(DISTINCT customer_id) FROM foodie_fi.subscriptions) AS count_customer,
	COUNT(customer_id) AS churned_straight,
	ROUND(COUNT(customer_id)::decimal/(SELECT COUNT(DISTINCT customer_id) FROM foodie_fi.subscriptions)*100) AS percentage_churned_straight
FROM ranked_cte
WHERE order_plan = 2 AND plan_id = 4 
```
##6. What is the number and percentage of customer plans after their initial free trial?
```sql
WITH ranked_cte AS (
SELECT 
	s.customer_id, 
	p.plan_id, 
	p.plan_name,
	LEAD(p.plan_id) OVER(PARTITION BY s.customer_id ORDER BY p.plan_id) AS next_plan_id
FROM foodie_fi.subscriptions AS s
JOIN foodie_fi.plans AS p
ON p.plan_id = s.plan_id
)

SELECT 
	next_plan_id,
	COUNT(customer_id) AS converted_customer,
	ROUND(COUNT(customer_id)::decimal/(SELECT COUNT(DISTINCT customer_id) FROM foodie_fi.subscriptions)*100) AS percentage_churned_straight
FROM ranked_cte
WHERE next_plan_id IS NOT NULL
GROUP BY next_plan_id
ORDER BY next_plan_id
```

##7. What is the customer count and percentage breakdown of all 5 plan_name values at 2020-12-31?
```sql
WITH ranked_cte AS (
SELECT 
	s.customer_id, 
	p.plan_id, 
	p.plan_name,
	LEAD(p.plan_id) OVER(PARTITION BY s.customer_id ORDER BY p.plan_id) AS next_plan_id
FROM foodie_fi.subscriptions AS s
JOIN foodie_fi.plans AS p
ON p.plan_id = s.plan_id
WHERE s.start_date <= '2020-12-31'
)

SELECT 
	plan_id, 
	plan_name,
	COUNT(customer_id) AS customer_each_plan,
	ROUND(COUNT(customer_id)::decimal/(SELECT COUNT(DISTINCT customer_id) FROM foodie_fi.subscriptions)*100,1) AS percentage_customer
FROM ranked_cte 
WHERE next_plan_id IS NULL
GROUP BY plan_id,  plan_name
ORDER BY plan_id
```

##8. How many customers have upgraded to an annual plan in 2020?
```sql
WITH ranked_cte AS (
SELECT 
	s.customer_id, 
	p.plan_id, 
	p.plan_name,
	LEAD(p.plan_id) OVER(PARTITION BY s.customer_id ORDER BY p.plan_id) AS next_plan_id,
	LEAD(s.start_date) OVER(PARTITION BY s.customer_id ORDER BY p.plan_id) AS next_start_date
FROM foodie_fi.subscriptions AS s
JOIN foodie_fi.plans AS p
ON p.plan_id = s.plan_id
)
	
SELECT 
	next_plan_id,
	COUNT(customer_id) AS customer_upgraded_anual
FROM ranked_cte 
WHERE next_plan_id = 3 AND DATE_PART('YEAR', next_start_date) = 2020
GROUP BY next_plan_id
ORDER BY next_plan_id
```

9. How many days on average does it take for a customer to upgrade to an annual plan from the day they join Foodie-Fi?
```sql
WITH trial_plan_cte AS (
    SELECT
        customer_id, 
        start_date AS trial_date
    FROM foodie_fi.subscriptions
    WHERE plan_id = 0 
),

upgraded_anual_cte AS (
    SELECT
        customer_id, 
        start_date AS annual_date
    FROM foodie_fi.subscriptions
    WHERE plan_id = 3 
)

SELECT 
    ROUND(AVG(annual.annual_date - trial.trial_date),0) AS avg_days_to_upgrade
FROM trial_plan_cte AS trial
JOIN upgraded_anual_cte AS annual
  ON trial.customer_id = annual.customer_id
```

##10. 

##11. 
```sql
WITH ranked_cte AS (
SELECT 
	s.customer_id, 
	p.plan_id, 
	p.plan_name,
	s.start_date,
	LEAD(p.plan_id) OVER(PARTITION BY s.customer_id ORDER BY s.start_date) AS next_plan_id
FROM foodie_fi.subscriptions AS s
JOIN foodie_fi.plans AS p
ON p.plan_id = s.plan_id
)

SELECT customer_id, plan_id, next_plan_id
FROM ranked_cte
WHERE DATE_PART('year', start_date) = 2020 
	AND plan_id = 2 
	AND next_plan_id =1
```

