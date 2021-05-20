# 1470. Shuffle the Array

## Approach 1: Iteration
Initialize an array that same length with `nums` and copy the number from the correct index in `nums` into the array.

```Java
class Solution {
    public int[] shuffle(int[] nums, int n) {
        int[] ans = new int[nums.length];
        
        int index = 0;
        for (int i = 0; i < n; i++) {
            ans[index++] = nums[i];
            ans[index++] = nums[i + n];
        }
        
        return ans;
    }
}
```

### Time and Space Complexity

N = length of the array `candies`
- Time: `O(N)`
- Space: `O(N)`

## References
- None