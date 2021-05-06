# 1693. Daily Leads and Partners

## Approach 1

```sql
SELECT 
    date_id, 
    make_name, 
    COUNT(DISTINCT(lead_id)) AS "unique_leads", 
    COUNT(DISTINCT(partner_id)) AS "unique_partners"
FROM DailySales
GROUP BY date_id, make_name;
```

### Time and Space Complexity
- None

## References
- None