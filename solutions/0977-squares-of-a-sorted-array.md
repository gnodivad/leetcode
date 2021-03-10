# 0977. Squares of a Sorted Array

## Approach 1: Two pointer
We use two pointers that will pointing to first and last element in the array respectively. Everytime find the largest value among the absolute value of two element that pointer pointed at, write the squared of that element into another array in reverse order.

```Java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int[] results = new int[nums.length];
    
        int left = 0, right = nums.length - 1;
        
        for (int idx = nums.length - 1; idx >= 0; idx--) {
            if (Math.abs(nums[left]) > Math.abs(nums[right])) {
                results[idx] = nums[left] * nums[left];
                left++;
            } else {
                results[idx] = nums[right] * nums[right];
                right--;
            }
        }
        
        return results;
    }
}
```

### Time and Space Complexity

N = length of the array `nums`
- Time: `O(N)`
- Space: `O(N)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Sorted%20Squared%20Array)