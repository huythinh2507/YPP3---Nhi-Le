```sql
CREATE FUNCTION GetSettingValue
(
    @category varchar(255),
	@variable varchar(255)
)
RETURNS TABLE
AS
RETURN
(
    SELECT
		setting_value
    FROM
        Setting
    WHERE 
        setting_type = @category and setting_name = @variable
);
```