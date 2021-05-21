# 1672. Richest Customer Wealth

## Approach 1: Iteration
Get the sum of the amount from all the bank account that each customer have and find the maximum among them.

```Java
class Solution {
    public int maximumWealth(int[][] accounts) {
        int max = Integer.MIN_VALUE;
        
        for (int i = 0; i < accounts.length; i++) {
            int total = 0;
            for (int j = 0; j < accounts[i].length; j++) {
                total += accounts[i][j];
            }
            max = Math.max(max, total);
        }
        
        return max;
    }
}
```

### Time and Space Complexity

M = total of customer, N = total of bank accounts
- Time: `O(MN)`
- Space: `O(1)`

## References
- None