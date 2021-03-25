# 1303. Find the Team Size

## Approach 1

```sql
SELECT
    e.employee_id, e2.team_size
FROM
    Employee e
LEFT JOIN (
    SELECT 
        team_id, count(team_id) as team_size
    FROM Employee
    GROUP BY team_id
) AS e2 ON e.team_id = e2.team_id;
```

### Time and Space Complexity
- None

## References
- None