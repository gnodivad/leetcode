# 0704. Binary Search

## Approach 1: Binary Search
When we search `target` in an sorted array, we can always use the middle element in the array as pivot. If the middle element is greater than our target, then we know the target is exist in the left side. Otherwise, it is on right side. Keep repeating this and adjust the left and right element accordingly until we find the target element.

```Java
class Solution {
    public int search(int[] nums, int target) {
        int low = 0, high = nums.length - 1;
        
        while (low <= high) {
            int medium = low + (high - low) / 2;
            
            if (nums[medium] == target) {
                return medium;
            } else if (nums[medium] > target) {
                high = medium - 1;
            } else {
                low = medium + 1;
            }
        }
        
        return -1;
    }
}
```

### Time and Space Complexity

N = length of nums
- Time: `O(log2(N))`
- Space: `O(1)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Binary%20Search)