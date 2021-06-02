# 0026. Remove Duplicates from Sorted Array

## Approach 1: Two Pointer
Maintains two pointer, `uniqueValueIndex` which points to the last index of result after remove duplicate and `scanIndex` that used to traverse the whole array. When different value encountered, increment the `uniqueValueIndex` and write the read data into the index.

```Java
class Solution {
    public int removeDuplicates(int[] nums) {
        int uniqueValueIndex = 0;
        int scanIndex = 1;
        
        while (scanIndex < nums.length) {
            if (nums[scanIndex] != nums[uniqueValueIndex]) {               
                nums[++uniqueValueIndex] = nums[scanIndex];
            }
            
            scanIndex++;
        }
        
        return uniqueValueIndex + 1;
    }
}
```

### Time and Space Complexity

N = Length of nums
- Time: `O(N)`
- Space: `O(1)`

## References
- None