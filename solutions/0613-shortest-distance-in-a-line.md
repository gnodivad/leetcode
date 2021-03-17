# 0613. Shortest Distance in a Line

## Approach 1

```sql
SELECT 
    MIN(ABS(p1.x - p2.x)) AS shortest 
FROM point p1, point p2 
WHERE p1.x != p2.x;
```

### Time and Space Complexity
- None

## References
- None