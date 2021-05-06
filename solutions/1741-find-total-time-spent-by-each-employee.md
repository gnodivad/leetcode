# 1741. Find Total Time Spent by Each Employee

## Approach 1

```sql
SELECT event_day AS day, emp_id, SUM(out_time - in_time) AS total_time
FROM Employees
GROUP BY emp_id, event_day;
```

### Time and Space Complexity
- None

## References
- None