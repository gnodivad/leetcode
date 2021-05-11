# 1480. Running Sum of 1d Array

## Approach 1: Iteration
Instead of recalculating the sum for all the num in the previous index, we can get the result for index `i` by simplying adding the element at index `i-1` which consist the sum up to index `i-1`.

```Java
class Solution {
    public int[] runningSum(int[] nums) {
        int runningSum = nums[0];
        
        for (int i = 1; i < nums.length; i++) {
            runningSum += nums[i];
            nums[i] = runningSum;
        }
        
        return nums;
    }
}
```

### Time and Space Complexity

N = length of the array `nums`
- Time: `O(N)`
- Space: `O(1)`

## References
- None