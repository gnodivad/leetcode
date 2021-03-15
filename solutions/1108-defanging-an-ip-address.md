# 1108. Defanging an IP Address

## Approach 1
Initialize StringBuilder to construct the string in efficient way because String itself is immutable. Scan through all character in the string, append character other than `.` to StringBuilder and append `[.]` if `.` is encountered.

```Java
class Solution {
    public String defangIPaddr(String address) {
        StringBuilder sb = new StringBuilder();
        
        for (char c : address.toCharArray()) {
            if (c == '.') {
                sb.append("[.]");
                continue;
            }
            
            sb.append(c);
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