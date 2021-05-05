# 0070. Climbing Stairs

## Approach 1: Recursion with Memoization
For every stair, we will either climbing 1 or 2 steps. The distinct ways will be the total of we climb one step now and two step now. To speed up the recusion, array `memo` will use to cache the distinct ways for each step to avoid re-computation.

```Java
class Solution {
    public int climbStairs(int n) {        
        int[] memo = new int[n + 1];
        memo[0] = 1;
        
        climbStairs(n, memo);
        
        return memo[n];
    }
    
    private int climbStairs(int n, int[] memo) {
        if (n < 0) return 0;
        
        if (memo[n] > 0) return memo[n];
        
        memo[n] = climbStairs(n - 1, memo) + climbStairs(n - 2, memo); 
        
        return memo[n];
    }
}
```

### Time and Space Complexity

N = length of the array `n`
- Time: `O(N)`
- Space: `O(N)`

## References
- None