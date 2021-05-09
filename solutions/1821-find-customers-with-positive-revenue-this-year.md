# 1821. Find Customers With Positive Revenue this Year

## Approach 1

```sql
SELECT customer_id
FROM Customers
WHERE year = 2021
GROUP BY customer_id
Having SUM(revenue) > 0;
```

### Time and Space Complexity
- None

## References
- None