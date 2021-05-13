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

## Approach 2: Dynamic Programming with optimized space
Looking at approach 1, we know that we just need to keep track of 2 rows. One row is for upper cell and another row is for left cell. The space can optimize further when we choose the lower value among `m` or `n` as x-axis.

```Java
class Solution {
    public int uniquePaths(int m, int n) {
        int y = m > n ? m : n;
		int x = m <= n ? m : n;
		
		int[] evenEdits = new int[x];
		int[] oddEdits = new int[x];
		
		for (int i = 0; i < x; i++) {
			evenEdits[i] = 1;
		}
		
		int[] currentEdits;
		int[] previousEdits;
		for (int i = 1; i < y; i++) {
			if (i % 2 == 0) {
				previousEdits = oddEdits;
				currentEdits = evenEdits;
			} else {
				previousEdits = evenEdits;
				currentEdits = oddEdits;
			}
			
			currentEdits[0] = 1;
			
			for (int j = 1; j < x; j++) {
				currentEdits[j] = previousEdits[j] + currentEdits[j - 1];
			}
		}
		
        return (y - 1) % 2 == 0 ? evenEdits[x - 1] : oddEdits[x - 1];
    }
}
```

### Time and Space Complexity

- Time: `O(M * N)`
- Space: `O(min(M, N))`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Number%20Of%20Ways%20To%20Traverse%20Graph)