# 1378. Replace Employee ID With The Unique Identifier

## Approach 1

```sql
Select EmployeeUNI.unique_id, Employees.name
FROM Employees
LEFT JOIN EmployeeUNI ON Employees.id = EmployeeUNI.id;
```

### Time and Space Complexity
- None

## References
- None