# 0595. Big Countries

## Approach 1

```sql
SELECT name, population, area
FROM World
WHERE area > 3000000 OR population > 25000000;
```

### Time and Space Complexity
- None

## References
- None