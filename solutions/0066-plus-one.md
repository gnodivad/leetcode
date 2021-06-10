# 0062. Unique Paths

## Approach 1: Dynamic Programming
Start with rightmost digit and add 1 to that array item. If the array item is less than 10, that meant we already solve the solution. Other, set that array item to 0 and continue to the left array item. Repeat this until the array item is iterate finish and we can initialize bigger array if we have carry left.

```Java
class Solution {
    public int[] plusOne(int[] digits) {
        boolean overflow = false;
        
        for (int i = digits.length - 1; i >= 0; i--) {
            digits[i] = digits[i] + 1;
            
            if (digits[i] == 10) {
                digits[i] = 0;
            } else {
                return digits;
            }
        }
        
        digits = new int[digits.length + 1];
        digits[0] = 1;
        
        return digits;
    }
}
```

### Time and Space Complexity

N = Length of the array `digits`
- Time: `O(N)`
- Space: `O(N)`

## References
- EPI 6.2