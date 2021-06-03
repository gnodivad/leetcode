# 0122. Best Time to Buy and Sell Stock II

## Approach 1: One Pass
Loop through the array from index `1` and add the difference of current price and previous price when the current price is greater than previous price.

```Java
class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0;
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1]) {
                profit += prices[i] - prices[i - 1];
            }
        }
        
        return profit;
    }
}
```

### Time and Space Complexity

N = Length of the array `prices`
- Time: `O(N)`
- Space: `O(1)`

## References
- None