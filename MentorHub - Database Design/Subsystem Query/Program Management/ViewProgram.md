![Untitled (34)](https://github.com/user-attachments/assets/e4d23bbd-44a6-4d6a-987f-b5b084af9853)

### Get recommended programs
```sql
WITH LatestTags AS (
    SELECT TOP 10 st.tag_id, COUNT(el.id) AS tag_count
    FROM EventLog el 
    JOIN SourceTag st ON el.source_id = st.source_id 
        AND el.source_type_id = st.source_type_id
    WHERE el.user_id = 1
    GROUP BY st.tag_id
    ORDER BY tag_count DESC
)
SELECT
    p.id, 
    p.program_name, 
    p.price, 
    p.description, 
    COUNT(r.source_id) AS review_count,
    AVG(r.rating_star) AS rating_star,
    COUNT(st.tag_id) AS tag_similar_count
FROM LatestTags lt
JOIN SourceTag st ON lt.tag_id = st.tag_id 
JOIN Program p ON st.source_id = p.id
LEFT JOIN Review r ON r.source_id = p.id AND r.source_type_id = (
    SELECT setting_value
    FROM GetSettingValue('SourceType', 'program')
)
GROUP BY p.id, p.program_name, p.price, p.description
ORDER BY tag_similar_count DESC;
```

### Get ads programs (*)
```sql
SELECT p.program_name, p.description, p.asset_id
FROM Ads AS a 
JOIN Program p ON a.source_id = p.id
WHERE a.source_type = (SELECT setting_value FROM GetSettingValue('SourceType', 'Program'))
AND a.start_at <= CURRENT_TIMESTAMP AND a.end_at >= CURRENT_TIMESTAMP;
```

### Get popular programs
```sql
SELECT 
    p.id, 
    p.program_name, 
    p.price, 
	COUNT(r.source_id) AS review_count,
    AVG(r.rating_star) AS rating_star,
    COUNT(el.user_id) AS view_count
FROM EventLog el
JOIN Program p ON el.source_id = p.id AND el.source_type_id = (
    SELECT setting_value
    FROM GetSettingValue('SourceType', 'program')
)
LEFT JOIN Review r ON r.source_id = p.id AND r.source_type_id = (
    SELECT setting_value
    FROM GetSettingValue('SourceType', 'program')
)
GROUP BY p.id, p.program_name, p.price
ORDER BY view_count DESC;
```
-- Get best-seller programs (*)
```sql
SELECT
    TOP 10 
    p.id, 
    p.program_name, 
    p.price, 
    COUNT(od.order_id) AS program_purchase_count 
FROM [Order] o
JOIN OrderDetail od ON o.id = od.order_id
JOIN Program p ON p.id = od.source_id
GROUP BY p.id, p.program_name, p.price
ORDER BY program_purchase_count DESC;
```

### Get trending program
```sql
WITH PopularProgram AS (
    SELECT 
		p.id, 
		p.program_name, 
		p.price, 
		COUNT(r.source_id) AS review_count,
		AVG(r.rating_star) AS rating_star,
		COUNT(el.user_id) AS view_count
	FROM EventLog el
	JOIN Program p ON el.source_id = p.id AND el.source_type_id = (
		SELECT setting_value
		FROM GetSettingValue('SourceType', 'program')
	)
	LEFT JOIN Review r ON r.source_id = p.id AND r.source_type_id = (
		SELECT setting_value
		FROM GetSettingValue('SourceType', 'program')
	)
	GROUP BY p.id, p.program_name, p.price
),
MonthlyEnrollments AS (
    SELECT 
        program_id, 
        FORMAT(start_at, 'yyyy-MM') AS month,
        COUNT(*) AS Enrollments
    FROM 
        ProgramUser
    GROUP BY 
        program_id, FORMAT(start_at, 'yyyy-MM')
),
MonthlyGrowth AS (
    SELECT 
		program_id,
		month,
		enrollments,
		LAG(enrollments) OVER (ORDER BY month) AS previous_month_enrollments,
		CASE
			WHEN LAG(enrollments) OVER (ORDER BY month) IS NULL THEN 0
			ELSE (enrollments - LAG(enrollments) OVER (ORDER BY month)) * 100.0 / LAG(enrollments) OVER (ORDER BY month)
		END AS growth_rate
	FROM 
		MonthlyEnrollments
	WHERE
		month = FORMAT(DATEADD(MONTH, 0, GETDATE()), 'yyyy-MM')
)

SELECT 
    pp.id, 
    pp.program_name, 
    pp.rating_star * 0.3 + pp.view_count * 0.3 + mg.growth_rate * 0.4 AS trend_score
FROM 
    PopularProgram pp
LEFT JOIN 
    MonthlyGrowth mg ON pp.id = mg.program_id
ORDER BY 
    trend_score DESC;
```
