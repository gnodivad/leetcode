# 0072. Edit Distance

## Approach 1: Dynamic Programming
Let compute the edit distance in a grid `dp`, y-axis is belongs to an empty character and each character of "HORSE" as `word1` and x-axis is belongs to an empty character and each character of ROS as `word2`. The `dp[0][0]` indicate the edit distance between two empty character, which is 0 since they are the same character. The edit distance will increase by 1 when moving to the right at the row 0 because each of the column indicate that the edit distance between an empty character to certain character of ROS [1...j]. This happen to the first column in grid, the edit distance will increase by 1 when we move to the bottom row by row.

If the character of both of the string is the same, the edit distance will be same as the edit distance before include both of the character, which is from `dp[i - 1][j - 1]`. Otherwise, the edit distance should the minimum of insertion `dp[i - 1][j - 1] + 1`, deletion from word1 `dp[i - 1][j] + 1` or replace an character `dp[i][j - 1] + 1`.

```Java
class Solution {
    public int minDistance(String word1, String word2) {
        int[][] dp = new int[word1.length() + 1][word2.length() + 1];
		
		for (int i = 0; i <= word1.length(); i++) {
			dp[i][0] = i;
		}
		
		for (int i = 0; i <= word2.length(); i++) {
			dp[0][i] = i;
		}
		
		for (int i = 1; i <= word1.length(); i++) {
			for (int j = 1; j <= word2.length(); j++) {
				if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
					dp[i][j] = dp[i - 1][j - 1];
				} else {
					dp[i][j] = Math.min(dp[i - 1][j - 1], Math.min(dp[i][j - 1], dp[i - 1][j])) + 1;
				}
			}
		}
		
		return dp[word1.length()][word2.length()];
    }
}
```

### Time and Space Complexity

M = length of the string `word1`, N = length of the string `word2`
- Time: `O(MN)`
- Space: `O(MN)`

## Approach 2: Dynamic Programming with space optimizing
In approach 1, the computation of each cells in the grid just need 3 neighbours cell, which are `dp[i - 1][j - 1]`, `dp[i][j - 1]`, and ``dp[i - 1][j]`. It meant that we just need to keep track two rows, one is current row `currentEdits` and previous row `previousEdits`. To save more space, we can use shorter word as x-axis and longer word as y-axis.

```Java
class Solution {
    public int minDistance(String word1, String word2) {
        String small = word1.length() < word2.length() ? word1 : word2;
		String big = word1.length() >= word2.length() ? word1 : word2;
		int[] evenEdits = new int[small.length() + 1];
		int[] oddEdits = new int[small.length() + 1];
		
		for (int j = 0; j <= small.length(); j++) {
			evenEdits[j] = j;	
		}
		
		int[] currentEdits;
		int[] previousEdits;
		for (int i = 1; i <= big.length(); i++) {
			if (i % 2 == 1) {
				currentEdits = oddEdits;
				previousEdits = evenEdits;
			} else {
				currentEdits = evenEdits;
				previousEdits = oddEdits;
			}
			
			currentEdits[0] = i;
			for (int j = 1; j <= small.length(); j++) {
				if (big.charAt(i - 1) == small.charAt(j - 1)) {
					currentEdits[j] = previousEdits[j - 1];
				} else {
					currentEdits[j] = 1 + Math.min(
						currentEdits[j - 1], 
						Math.min(previousEdits[j - 1], previousEdits[j])
					);
				}
			}
		}
		
		return big.length() % 2 == 0 ? evenEdits[small.length()] : oddEdits[small.length()];
    }
}
```

### Time and Space Complexity

M = length of the string `word1`, N = length of the string `word2`
- Time: `O(MN)`
- Space: `O(min(N, M))`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Levenshtein%20Distance)