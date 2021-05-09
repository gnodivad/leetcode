# 1581. Customer Who Visited but Did Not Make Any Transactions

## Approach 1

```sql
SELECT customer_id, COUNT(Visits.visit_id) AS count_no_trans
FROM Visits
LEFT JOIN Transactions ON Visits.visit_id = Transactions.visit_id
WHERE transaction_id iS NULL
GROUP BY customer_id;
```

### Time and Space Complexity
- None

## References
- None