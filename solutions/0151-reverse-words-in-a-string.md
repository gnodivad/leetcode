# 0151. Reverse Words in a String

## Approach 1: Recursive
Reverse the whole string follow by reverse word by word.

```Java
class Solution {
    public String reverseWords(String s) {
        s = s.trim();
        
        StringBuilder sb = new StringBuilder();
        
        int index = 0;
        while (index < s.length()) {
            while (index < s.length() - 1 && s.charAt(index) == ' ' && s.charAt(index + 1) == ' ') index++;
        
            sb.insert(0, s.charAt(index));
            
            index++;
        }
        
        int n = sb.length();
        int start = 0, end = 0;
        
        while (start < n) {
            while (end < n && sb.charAt(end) != ' ') ++end;
    
            reverse(sb, start, end - 1);        
            start = end + 1;
            end++;
        }
        
        return sb.toString();
    }
    
    public void reverse(StringBuilder sb, int left, int right) {
        while (left < right) {
            char tmp = sb.charAt(left);
            sb.setCharAt(left++, sb.charAt(right));
            sb.setCharAt(right--, tmp);
        }
    }
}
```

### Time and Space Complexity

N = Length of s
- Time: `O(N)`
- Space: `O(N)`

## References
- EPI 7.6