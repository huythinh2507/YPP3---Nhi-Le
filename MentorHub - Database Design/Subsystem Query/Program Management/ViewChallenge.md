### ERD
![View Program](https://github.com/user-attachments/assets/b457d7e6-fdae-4947-b4a5-4d06ea869a6a)

### Get recommended challenge (*)
```sql
WITH LatestTags AS (
    SELECT TOP 10 st.tag_id, COUNT(el.id) tag_count
	FROM EventLog el JOIN SourceTag st ON el.source_id = st.source_id AND el.source_type_id = st.source_type_id
	WHERE user_id = 1
	GROUP BY st.tag_id
	ORDER BY tag_count DESC
)

SELECT
    ch.challenge_name,
	COUNT(st.tag_id) AS tag_simlar_count
FROM LatestTags lt
JOIN SourceTag st ON lt.tag_id = st.tag_id 
JOIN challenge ch ON st.source_id = ch.id
GROUP BY ch.challenge_name
ORDER BY tag_simlar_count DESC
```

### Get popular challenges
```sql
SELECT cl.id, cl.challenge_name, COUNT(el.user_id) view_count
FROM EventLog el
	JOIN Challenge cl ON el.source_id = cl.id AND el.source_type_id = (
        SELECT setting_value
		FROM GetSettingValue('SourceType', 'challenge')
    )
GROUP BY cl.id, cl.challenge_name
ORDER BY view_count DESC
```
  
### Upcoming in 24 hours (*)
```sql
SELECT
	cl.challenge_name,
    cl.location,
    cl.start_date
FROM
	Challenge cl
WHERE 
	cl.start_date BETWEEN CURRENT_TIMESTAMP AND DATEADD(day, 1, CURRENT_TIMESTAMP)
ORDER BY
	cl.start_date DESC
```
