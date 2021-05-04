# 0387. First Unique Character in a String

## Approach 1
Iterate through string `s` character by character and building a frequency counts for each character. Then we go through the string second time and check for the count of each character. Return the index if current character's count in the array we build earlier is `1`.

```Java
class Solution {
    public int firstUniqChar(String s) {
        int[] counts = new int[26];
		
		for (char c : s.toCharArray()) {
			counts[c - 'a']++;
		}
		
		for (int i = 0; i < s.length(); i++) {
			if (counts[s.charAt(i) - 'a'] == 1) {
				return i;
			}
		}
		
        return -1;
    }
}
```

### Time and Space Complexity

N = length of the string `s`
- Time: `O(N)`
- Space: `O(1)`
