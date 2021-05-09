# 1571. Warehouse Manager

## Approach 1

```sql
SELECT name as warehouse_name, SUM(Width * Length * Height * units) as volume
FROM Warehouse
LEFT JOIN Products ON Warehouse.product_id = Products.product_id
GROUP BY name;
```

### Time and Space Complexity
- None

## References
- None