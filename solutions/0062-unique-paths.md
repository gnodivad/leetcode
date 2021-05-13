# 0062. Unique Paths

## Approach 1: Dynamic Programming
Let have a grid with size `m * n` to keep track number of ways to reach each of the cell. The cells in first row and first column will filled with 1 because we only have 1 ways to reach them either by move right or move down. Let say we are computing for cell `(m, n)`, the ways to reaching it either from upper cell `(m - 1, n)` or left cell `(m, n -1)`. That meant that the total number of paths to move into `(m, n)` defined as `uniquePaths(m, n) = uniquePath(m - 1, n) + uniquePath(m, n - 1)`.

```Java
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];
		
		for (int i = 0; i < m; i++) {
			dp[i][0] = 1;
		}
		
		for (int i = 0; i < n; i++) {
			dp[0][i] = 1;
		}		
		
		for (int i = 1; i < m; i++) {
			for (int j = 1; j < n; j++) {
				dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
			}
		}
				
        return dp[m - 1][n - 1];
    }
}
```

### Time and Space Complexity

- Time: `O(M * N)`
- Space: `O(M * N)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Number%20Of%20Ways%20To%20Traverse%20Graph)