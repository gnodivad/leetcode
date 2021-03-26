# 1350. Students With Invalid Departments

## Approach 1

```sql
SELECT
    Students.id,
    Students.name
FROM Students
LEFT JOIN Departments ON Students.department_id = Departments.id
WHERE Departments.id IS NULL;
```

### Time and Space Complexity
- None

## References
- None