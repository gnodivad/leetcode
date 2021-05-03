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


## Approach 2: Bottom up Approach
Compute all minimum counts for amounts up to `i` and store it in index `i` of an array `minChanges`. In another words, `minChanges[3]` is the minimum counts for `3` as amounts. If we have three coins, which are `c1`, `c2`, and `c3`. The `minChanges[3]` will be `min(minChanges[3 - c1], minChanges[3 - c2], minChanges[3 - c3]) + 1`.

```Java
class Solution {
    public int coinChange(int[] coins, int amount) {
        int[] minChanges = new int[amount + 1];
        Arrays.fill(minChanges, amount + 1);
        minChanges[0] = 0;
        
        for (int i = 1; i <= amount; i++) {
            for (int coin : coins) {
                if (i < coin) continue;
                
                minChanges[i] = Math.min(minChanges[i], 1 + minChanges[i - coin]);
            }
        }
        
        return minChanges[amount] > amount ? -1 : minChanges[amount];
    }
}
```

### Time and Space Complexity

N = Length of array `coins`, A is the `amount`
- Time: `O(N * A)`
- Space: `O(A)`