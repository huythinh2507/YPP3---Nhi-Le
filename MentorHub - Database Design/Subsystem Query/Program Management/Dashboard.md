### ERD
<img src="https://github.com/user-attachments/assets/9293d3ae-c21d-4194-8c14-ed0a5c2a55cd" height="500">
### Get all programs and completed programs of user 2
```sql
SELECT
	COUNT(program_id) AS total_program,
    SUM(CASE WHEN status = 'Completed' THEN 1 ELSE 0 END) AS completed_program
FROM
	ProgramUser
WHERE 
	user_id = 2;
```

### Get all challenges and completed challenges of user 2
```sql
SELECT
	COUNT(challenge_id) AS total_challenge,
    SUM(CASE WHEN status = 'Passed' THEN 1 ELSE 0 END) AS completed_challenge
FROM
	ChallengeUser
WHERE 
	user_id = 2;
```

### Get program progress
```sql
SELECT
	p.[program_name], 
    u.[name] AS mentor_name,
    pu.progress_percent,
    pu.status
FROM 
	ProgramUser pu 
    JOIN Program p ON pu.program_id = p.id
    JOIN [User] u ON p.[user_id] = u.id
WHERE 
	pu.[user_id] = 2;
```

### Get challenge progress
```sql
SELECT
	c.challenge_name AS challenge_name,
    c.location AS challenge_location
FROM 
	ChallengeUser cu 
    JOIN Challenge c ON cu.challenge_id = c.id
WHERE 
	cu.[user_id] = 2
ORDER BY
	cu.date_submission;
```

### Get average hour activity of user 2 (*)
```sql
WITH month_12_year AS (
	SELECT 1 as month_year
	UNION ALL
	SELECT month_year + 1
	FROM month_12_year
	WHERE month_year < 12
),
get_month AS (
SELECT 
	*,
	MONTH(online_date) as date_calendar
FROM UserOnline
)

SELECT 
	m12y.month_year,
	SUM(CONVERT(float,REPLACE(LEFT(online_time, 5), ':', '.')))/
	DATEDIFF(dd, GETDATE(), DATEADD(mm, month_year, GETDATE())) as avg_time
FROM get_month gm
RIGHT JOIN month_12_year m12y ON gm.date_calendar = m12y.month_year
GROUP BY m12y.month_year
```
