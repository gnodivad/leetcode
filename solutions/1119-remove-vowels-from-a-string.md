# 1119. Remove Vowels from a String

## Approach 1
Initialize StringBuilder to construct the string in efficient way because String itself is immutable. Scan through all character in the string and append non-vowel character to StringBuilder.

```Java
class Solution {
    public String removeVowels(String s) {
        StringBuilder sb = new StringBuilder();
        
        for (char c : s.toCharArray()) {
            if (c != 'a' && c != 'e' && c != 'i' && c != 'o' && c != 'u') {
                sb.append(c);
            }
        }
        
        return sb.toString();
    }
}
```

### Time and Space Complexity

N = length of the string
- Time: `O(N)`
- Space: `O(1)`

## References
- None