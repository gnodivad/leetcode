# 1464. Maximum Product of Two Elements in an Array

## Approach 1: Iteration
The maximum product in the array must be the product of two the most maximum two number in the array. So we just declare two variable to keep track two maximum value.

```Java
class Solution {
    public int maxProduct(int[] nums) {
        int max = Integer.MIN_VALUE, secondMax = Integer.MIN_VALUE;
        
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] > max) {
                secondMax = max;
                max = nums[i];
            } else if (nums[i] > secondMax) {
                secondMax = nums[i];
            }
        }
                
        return (max - 1) * (secondMax - 1);
    }
}
```

### Time and Space Complexity

N = length of the array `arr`
- Time: `O(N)`
- Space: `O(1)`

## References
- None