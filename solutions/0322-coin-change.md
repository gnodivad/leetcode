# 0322. Coin Change

## Approach 1: Top Down Approach
The approach will break the target `amount` into smaller amount by subtracting every coin we have. Two base case we will have by doing this:
1. The new amount will be `0`. In this case, we just return `0` because we found a combination of coin change.
2. The new amount will be negative. In this case, we just return `-1` to indicate that current combination is incorrect.
When subtracting every coin from the `amount`, we also need to keep track the minimum change `min` and return to the parent function.

```Java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int[] memo = new int[amount + 1];
        return coinChange(coins, amount, memo);
    }
    
    public int coinChange(int[] coins, int amount, int[] memo) {
        if (amount == 0) return 0;
        if (amount < 0) return -1;
        
        if (memo[amount] != 0) return memo[amount];
        
        int min = Integer.MAX_VALUE;
        for (int coin: coins) {
            int change = coinChange(coins, amount - coin, memo);
            
            if (change >= 0 && change < min) {
                min = 1 + change;
            }
        }
        
        memo[amount] = min == Integer.MAX_VALUE ? -1 : min;
        return memo[amount];
    }
}
```

### Time and Space Complexity

N = Length of array `coins`, A is the `amount`
- Time: `O(N * A)`
- Space: `O(A)`
