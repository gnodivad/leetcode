# 1587. Bank Account Summary II

## Approach 1

```sql
SELECT Users.name, SUM(amount) AS balance
FROM Users
LEFT JOIN Transactions ON Users.account = Transactions.account
GROUP BY Users.account
Having balance >= 10000;
```

### Time and Space Complexity
- None

## References
- None