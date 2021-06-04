# 0034. Find First and Last Position of Element in Sorted Array

## Approach 1: Binary Search
Apply two binary search in the sorted array to find the first and last occurences index. To find the first occurences, just check the `medium == begin` and `nums[medium - 1]` still consist of same target. To find the last occurences, just check the `medium == end` and the next item in the array has the same target.

```Java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int firstOccurrence = this.findBound(nums, target, true);
        
        if (firstOccurrence == -1) {
            return new int[]{-1, -1};
        }
        
        int lastOccurrence = this.findBound(nums, target, false);
        
        return new int[]{firstOccurrence, lastOccurrence};
    }
    
    private int findBound(int[] nums, int target, boolean isFirst) {
        int begin = 0, end = nums.length - 1;
        
        while (begin <= end) {
            int mid = begin + (end - begin) / 2;
            
            if (nums[mid] == target) {
                if (isFirst) {
                    if (mid == begin || nums[mid - 1] != target) return mid;
                    end = mid - 1;
                } else {
                    if (mid == end || nums[mid + 1] != target) return mid;
                    begin = mid + 1;
                }
            } else if (nums[mid] > target) {
                end = mid - 1;
            } else {
                begin = mid + 1;
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
- EPI 12.1