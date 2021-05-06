# 1683. Invalid Tweets

## Approach 1

```sql
SELECT tweet_id
FROM Tweets
WHERE length(content) > 15;
```

### Time and Space Complexity
- None

## References
- None