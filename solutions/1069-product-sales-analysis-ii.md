# 1069. Product Sales Analysis II

## Approach 1

```sql
SELECT
    s.product_id,
    SUM(s.quantity) as "total_quantity"
FROM Sales s
LEFT JOIN Product p ON p.product_id = s.product_id
GROUP BY s.product_id;
```

### Time and Space Complexity
- None

## References
- None