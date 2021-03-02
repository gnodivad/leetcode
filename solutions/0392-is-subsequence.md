# 0392. Is Subsequence

## Approach 1: Two Pointers
We use two pointers that will pointing to first element of `s` and `t`. If the character in `s` is same as `t`, we move both the pointer to next character in the string. Otherwise, we just move the pointer in the longest string.

```Java
class Solution {
    public boolean isSubsequence(String s, String t) {
        int sPtr = 0, tPtr = 0;
		
		while (sPtr < s.length() && tPtr < t.length()) {
			if (s.charAt(sPtr) == t.charAt(tPtr)) {
				sPtr++;
			}
			
			tPtr++;
		}
		
        return sPtr == s.length();
    }
}
```

### Time and Space Complexity

- Time: `O(n)`
- Space: `O(1)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Validate%20Subsequence)