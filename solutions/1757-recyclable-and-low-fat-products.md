# 1757. Recyclable and Low Fat Products

## Approach 1

```sql
SELECT 
    product_id 
FROM Products 
WHERE low_fats = 'Y' and recyclable = 'Y';
```

### Time and Space Complexity
- None

## References
- None