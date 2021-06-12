# 0443. String Compression

## Approach 1: Look-ahead and Write
We will use seperate pointers, `read` and `write` to indicate where we reading from and writing to in the array. Besides that, we also mantain `anchor` that used to mark on the end of contigious group. When the current `read` is the last index or the current `read` character is different from the next `read` character, this meant that it is the end of the contigious group. The length of this group will be `read - anchor + 1`.


```java
class Solution {
    public int compress(char[] chars) {
        int anchor = 0, write = 0;
        
        for (int read = 0; read < chars.length; read++) {
            if (read + 1 == chars.length || chars[read] != chars[read + 1]) {
                chars[write++] = chars[anchor];
                
                if (read > anchor) { 
                    for (char c : ("" +  (read - anchor + 1)).toCharArray()) {
                        chars[write++] = c;
                    }
                }
                
                anchor = read + 1;
            }
        }
        
        return write;
    }
}
```

### Time and Space Complexity
N = Length of the array `chars`
- Time: `O(N)`
- Space: `O(1)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Run-Length%20Encoding)