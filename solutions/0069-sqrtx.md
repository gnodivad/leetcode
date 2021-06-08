# 0069. Sqrt(x)

## Approach 1: Binary Search
Since the valid square root for a number `x` will be `2 < a < x/2`, we can use binary search to navigate through the number between `2` and `x/2`. Number `left - 1` will be returned if the exact square root for `x` cannot be found.

```Java
class Solution {
    public int mySqrt(int x) {
        if (x < 2) return x;
        
        long num;
        int pivot, left = 2, right = x / 2;
        
        while (left <= right) {
            pivot = left + (right - left) / 2;
            num = (long)pivot * pivot;
            if (num > x) right = pivot - 1;
            else if (num < x) left = pivot + 1;
            else return pivot;
        }
        
        return left - 1;
    }
}
```

### Time and Space Complexity

- Time: `O(Log(N))`
- Space: `O(1)`

## References
- EPI 12.4