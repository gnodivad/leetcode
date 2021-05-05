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


## Approach 2: Dynamic Programming
The problem can broken into subproblems, and optimal solution can be constructed efficiently from optimal solutions of its subproblem. Everyone can reach `ith` by following way:
1. Taking a single step from `(i - 1)th step`
2. Taking a step of 2 from `(i - 2)th step`
So, the total number of ways to reach `ith` is equal to sum of ways of reach `(i - 1)th` step and ways of reaching `(i - 2)th` step.
`dp[i] = dp[i - 1] + dp[i - 2]`

```Java
class Solution {
    public int climbStairs(int n) {     
        if (n == 1) {
            return 1;
        }
        
        int[] dp = new int[n + 1];
        dp[1] = 1;
        dp[2] = 2;
        
        for (int i = 3; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        
        return dp[n];
    }
}
```

### Time and Space Complexity

N = length of the array `n`
- Time: `O(N)`
- Space: `O(N)`

## References
- None