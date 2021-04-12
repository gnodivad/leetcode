# 0627. Swap Salary

## Approach 1

```sql
UPDATE SALARY
SET sex = IF(sex = 'm', 'f', 'm') WHERE sex IN ('m', 'f');
```

### Time and Space Complexity
- None

## References
- None