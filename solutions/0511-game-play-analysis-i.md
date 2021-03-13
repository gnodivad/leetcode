# 0511. Game Play Analysis I

## Approach 1

```sql
SELECT
    player_id,
    MIN(event_date) AS first_login
FROM Activity
GROUP BY
    player_id;
```

### Time and Space Complexity
- None

## References
- None