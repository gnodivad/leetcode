# 0121. Best Time to Buy and Sell Stock

## Approach 1: Dynamic Programming
Let assume that the price for first day is the price we bought the stock and store it as `min` and `maxProfit` is `0`. For the incoming day, the decision that we need to make are:
1. Buy the stock
2. Sell the stock
We will get the maximum profit if we buy the stock at lowest price and sell the stock at highest price. Everyday we sell the stock and record it if the profit is greater than current `maxProfit`. If the price of stock for today we see is lower than the price we saw before, we will store it in `min` so we can increase the profit afterwards.

```Java
class Solution {
    public int maxProfit(int[] prices) {
        int min = prices[0];
        int maxProfit = 0;
        
        for (int i = 1; i < prices.length; i++) {
            maxProfit = Math.max(maxProfit, prices[i] - min);
            min = Math.min(min, prices[i]);
        }
        
        return maxProfit;
    }
}
```

### Time and Space Complexity

N = number of node in the tree
- Time: `O(N)`
- Space: `O(1)`

## References
- None