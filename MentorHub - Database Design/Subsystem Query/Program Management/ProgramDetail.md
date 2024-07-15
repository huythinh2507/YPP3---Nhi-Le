### ERD
![Program Detail](https://github.com/user-attachments/assets/0cbd4169-7d83-49b9-98be-f3e997893266)

### Get program details
```sql
SELECT 
    p.program_name,
    p.description,
    p.price,
    u.[name] AS mentor_name,
    p.asset_id,
    COUNT(r.source_id) AS review_count,
    AVG(r.rating_star) AS rating_star
FROM 
    Program p
    JOIN [User] u ON p.user_id = u.id
    LEFT JOIN Review r ON r.source_id = p.id AND r.source_type_id = (
        SELECT setting_value
		FROM GetSettingValue('SourceType', 'program')
    )
WHERE 
    p.id = 2
GROUP BY
    p.program_name, p.description, p.price, u.[name], p.asset_id
```

### Get images of a program (*)
```sql
SELECT source_id, asset_id
FROM SourceImage 
WHERE source_id = 1 AND source_type_id = (
    SELECT setting_value
    FROM GetSettingValue('SourceType', 'program')
)
```

### Get challenge of a program
```sql
SELECT
    cl.id,
    cl.challenge_name,
    cl.description,
    ps.source_order
FROM
    Challenge cl
    JOIN ProgramSource ps ON cl.id = ps.source_id AND ps.source_type_id = (
        SELECT setting_value
		FROM GetSettingValue('SourceType', 'challenge')
    )
WHERE
    ps.program_id = 2
```

### Get course of a program
```sql
SELECT
    c.id,
    c.name,
    c.description,
    ps.source_order
FROM
    Course c
    JOIN ProgramSource ps ON c.id = ps.source_id AND ps.source_type_id = (
        SELECT setting_value
		FROM GetSettingValue('SourceType', 'course')
    )
WHERE 
    ps.program_id = 2
```
