```sql
CREATE FUNCTION dbo.GetViewSource(@user_id INT)
RETURNS TABLE
AS
RETURN
(
    WITH get_view AS
    (
        SELECT
            l.[user_id],
            ld.event_parameter_id,
            ld.value,
            l.log_time
        FROM
            [Log] l
        LEFT JOIN [EventType] et ON et.id = l.event_type_id AND et.name = 'View'
        LEFT JOIN [EventParameter] ep ON ep.event_type_id = et.id
        LEFT JOIN LogDetail ld ON ld.log_id = l.id AND ld.event_parameter_id = ep.id
    ),
    get_source AS
    (
        SELECT
            [value] AS source_id,
            log_time
        FROM
            get_view
        WHERE event_parameter_id = 4 AND [user_id] = @user_id
    )
    SELECT source_id, log_time
    FROM get_source
);
GO

```