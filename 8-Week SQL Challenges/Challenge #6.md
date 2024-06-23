# A. Digital Analysis
## 1. How many users are there?
```sql
SELECT 
  COUNT(DISTINCT user_id) AS count_user
FROM clique_bait.users
```

## 2. How many cookies does each user have on average?
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