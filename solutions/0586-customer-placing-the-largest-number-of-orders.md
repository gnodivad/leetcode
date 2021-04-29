# 586. Customer Placing the Largest Number of Orders

## Approach 1

```sql
SELECT
    customer_number
FROM
    orders
GROUP BY customer_number
ORDER BY COUNT(*) DESC
LIMIT 1;
```

### Time and Space Complexity
- None

## References
- None