## Case Study #5: Data Mart
- [Case Study #5: Data Mart](https://8weeksqlchallenge.com/case-study-5/)
- [Reference Answer](https://github.com/katiehuangx/8-Week-SQL-Challenge/tree/main/Case%20Study%20%235%20-%20Data%20Mart)

***

## 📚 My Solution
## A. Data Cleansing Steps
```sql
DROP TABLE IF EXISTS clean_weekly_sales;
CREATE TEMP TABLE clean_weekly_sales AS (
SELECT
	TO_DATE(week_date, 'DD/MM/YY') AS week_date,
	EXTRACT(WEEK FROM TO_DATE(week_date, 'DD/MM/YY')) AS week_number,
	EXTRACT(MONTH FROM TO_DATE(week_date, 'DD/MM/YY')) AS month_number,
	EXTRACT(YEAR FROM TO_DATE(week_date, 'DD/MM/YY')) AS calendar_year,
	region, 
	platform,
	segment,
	CASE 
		WHEN RIGHT(segment, 1) = '1' THEN 'Young Adults' 
		WHEN RIGHT(segment, 1) = '2' THEN 'Middle Aged'
		WHEN RIGHT(segment, 1) IN ('3', '4') THEN 'Retirees' 
		ELSE 'Unknown' END AS age_band,
	CASE 
		WHEN LEFT(segment, 1) = 'C' THEN 'Couples'
		WHEN LEFT(segment, 1) = 'F' THEN 'Families'
		ELSE 'Unknown' END AS demographics, 
	transactions,
	ROUND((sales::NUMERIC/transactions),2) AS avg_transaction,
	sales
FROM data_mart.weekly_sales
);

SELECT * FROM clean_weekly_sales
```

## B. Data Exploration
### 1. What day of the week is used for each week_date value?
```sql
SELECT DISTINCT TO_CHAR(week_date, 'Day') AS week_date
FROM clean_weekly_sales
```

### 2. What range of week numbers are missing from the dataset?
```sql
WITH week_number_cte AS (
	SELECT GENERATE_SERIES(1,52) AS week_num
)

SELECT wn.week_num, cws.week_number
FROM week_number_cte AS wn 
LEFT JOIN clean_weekly_sales AS cws
ON cws.week_number = wn.week_num
WHERE week_number IS NULL
ORDER BY week_num
```

### 3. How many total transactions were there for each year in the dataset?
```sql
SELECT 
	calendar_year, 
	SUM(transactions) as totol_transaction
FROM clean_weekly_sales
GROUP BY calendar_year
ORDER BY calendar_year
```

### 4. What is the total sales for each region for each month?
```sql
SELECT 
	region,
	month_number,
	SUM(sales) AS total_sales
FROM clean_weekly_sales
GROUP BY region, month_number
ORDER BY region, month_number
```

### 5. What is the total count of transactions for each platform?
```sql
SELECT 
	platform,
	SUM(transactions) as total_transactions
FROM clean_weekly_sales
GROUP BY platform
ORDER BY platform
```

### 6. What is the percentage of sales for Retail vs Shopify for each month?
```sql
SELECT 
	calendar_year,
	month_number,
	ROUND(100 * SUM(CASE WHEN platform = 'Retail' THEN sales END)::decimal/SUM(sales),2) AS retail_percentage,
	ROUND(100 * SUM(CASE WHEN platform = 'Shopify' THEN sales END)::decimal/SUM(sales),2) AS shopify_percentage	
FROM clean_weekly_sales
GROUP BY calendar_year, month_number
ORDER BY calendar_year, month_number
```

### 7. What is the percentage of sales by demographic for each year in the dataset?
```sql
SELECT 
	calendar_year,
	ROUND(100 * SUM(CASE WHEN demographics = 'Unknown' THEN sales END)::decimal/SUM(sales),2) AS unknown_percentage,
	ROUND(100 * SUM(CASE WHEN demographics = 'Couples' THEN sales END)::decimal/SUM(sales),2) AS couples_percentage,
	ROUND(100 * SUM(CASE WHEN demographics = 'Families' THEN sales END)::decimal/SUM(sales),2) AS families_percentage
FROM clean_weekly_sales 
GROUP BY calendar_year
ORDER BY calendar_year
```

### 8. Which age_band and demographic values contribute the most to Retail sales?
```sql
SELECT 
  age_band, 
  demographic, 
  SUM(sales) AS retail_sales,
  ROUND(100 * SUM(sales)::NUMERIC / SUM(SUM(sales)) OVER (), 1) AS contribution_percentage
FROM clean_weekly_sales
WHERE platform = 'Retail'
GROUP BY age_band, demographic
ORDER BY retail_sales DESC
```

### 9. Can we use the avg_transaction column to find the average transaction size for each year for Retail vs Shopify? If not - how would you calculate it instead?
```sql
```

## C. Before & After Analysis
### 1. What is the total sales for the 4 weeks before and after 2020-06-15? What is the growth or reduction rate in actual values and percentage of sales?
```sql
WITH week_number AS (
SELECT 
	week_number,
	SUM(sales) as total_sales
FROM clean_weekly_sales
WHERE week_date BETWEEN ('2020-06-15'::DATE - INTERVAL '4 WEEKS')
				AND ('2020-06-15'::DATE + INTERVAL '3 WEEKS')
GROUP BY week_number
ORDER BY week_number
),
	
before_after_changes AS (
SELECT 
	SUM(CASE WHEN week_number < DATE_PART('week', '2020-06-15'::DATE) THEN total_sales END) AS before_changes,
	SUM(CASE WHEN week_number >= DATE_PART('week', '2020-06-15'::DATE) THEN total_sales END) AS after_changes
FROM week_number
)

SELECT 
	after_changes - before_changes AS sale_variance,
	ROUND(100 * (after_changes - before_changes)::decimal/before_changes, 2) || '%' AS variance_percentage 
FROM before_after_changes
```

### 2. What about the entire 12 weeks before and after?
```sql
--Method 1:
WITH week_number AS (
SELECT 
	week_number,
	SUM(sales) as total_sales
FROM clean_weekly_sales
WHERE week_date BETWEEN ('2020-06-15'::DATE - INTERVAL '12 WEEKS')
				AND ('2020-06-15'::DATE + INTERVAL '11 WEEKS')
GROUP BY week_number
ORDER BY week_number
),
	
before_after_changes AS (
SELECT 
	SUM(CASE WHEN week_number < DATE_PART('week', '2020-06-15'::DATE) THEN total_sales END) AS before_changes,
	SUM(CASE WHEN week_number >= DATE_PART('week', '2020-06-15'::DATE) THEN total_sales END) AS after_changes
FROM week_number
)

SELECT 
	after_changes - before_changes AS sale_variance,
	ROUND(100 * (after_changes - before_changes)::decimal/before_changes, 2) || '%' AS variance_percentage 
FROM before_after_changes
```

```sql
-- Method 2:

--Create variable for baseline date
WITH date_baseline AS (
    SELECT '2020-06-15'::DATE AS date
),

week_sales AS (
    SELECT 
        cws.week_number,
        SUM(cws.sales) AS total_sales
    FROM clean_weekly_sales AS cws, 
		 date_baseline as db
    WHERE cws.week_date BETWEEN (db.date - INTERVAL '12 WEEKS') 
                        AND (db.date + INTERVAL '11 WEEKS')
    GROUP BY cws.week_number
    ORDER BY cws.week_number
),

before_after_changes AS (
    SELECT 
        SUM(CASE WHEN w.week_number < DATE_PART('week',db.date) THEN total_sales ELSE 0 END) AS before_changes,
        SUM(CASE WHEN w.week_number >= DATE_PART('week', db.date) THEN total_sales ELSE 0 END) AS after_changes
    FROM week_sales as w, date_baseline as db
)

SELECT 
    after_changes - before_changes AS sale_variance,
    ROUND(100 * (after_changes - before_changes)::decimal / before_changes, 2) || '%' AS variance_percentage 
FROM before_after_changes;
```

### 3. How do the sale metrics for these 2 periods before and after compare with the previous years in 2018 and 2019?
```sql
```

## D. Bonus Question
```sql
```

