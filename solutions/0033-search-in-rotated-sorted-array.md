# 0033. Search in Rotated Sorted Array

## Approach 1: Binary Search
Use Binary Search to find the `target`. Every iteration of binary search, the pivot `medium` will divide the array into half. The array will ends out split into one with the sorted array and another one with non-sorted array. If the `nums[medium] >= nums[left]`, the array item in index `left` to `medium` is sorted array. If the target is within the range, it should be on exist in the sorted array. Otherwise, it will exist in another half of the array. If the `nums[medium] < nums[left]`, the array item in index `medium` to `right` is sorted array. Same logic as before to use to determine which next subarray used to find the target.

```Java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        
        while (left <= right) {
            int medium = left + (right - left) / 2;
            
            if (nums[medium] == target) {
                return medium;
            } else if (nums[medium] >= nums[left]) {
                if (target >= nums[left] && target < nums[medium]) {
                    right = medium - 1;
                } else {
                    left = medium + 1;
                }
            } else {
                if (target <= nums[right] && target > nums[medium]) {
                    left = medium + 1;
                } else {
                    right = medium - 1;
                }
            }
        }
        
        return -1;
    }
}
```

### Time and Space Complexity

N = Length of nums
- Time: `O(Log(N))`
- Space: `O(1)`

## References
- None