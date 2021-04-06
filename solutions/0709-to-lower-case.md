# 0709. To Lower Case

## Approach 1
Implement two function, one is used to check the character is between `A` and `Z` and another one is covert the uppercase character into corresponding lowercase character. Since `a = A + 32`, it meant that we just need to flip the bit of `2 ^ 5` to 1.

```Java
class Solution {
    public boolean isUpper(char x) {
        return 'A' <= x && x <= 'Z';
    }
    
    public char toLower(char x) {
        return (char)((int)x | 32);
    }
    
    public String toLowerCase(String str) {
        StringBuilder sb = new StringBuilder();
        
        for (char c : str.toCharArray()) {
            sb.append(isUpper(c) ? toLower(c) : c);
        }
        
        return sb.toString();
    }
}
```

### Time and Space Complexity

N = length of the string `str`
- Time: `O(N)`
- Space: `O(N)`

## References
- None