# 0162. Find Peak Element

## Approach 1: Linear Scan
Loop through the array `nums`, check the right neighbour in the arr is smaller than current number and return it if found. Otherwise, return the last element in the element. The latter scenario is applied when the array is contains all increasing element `[1, 2, 3]` and the array contains only one element `[1]`.

```Java
class Solution {
    public int findPeakElement(int[] nums) {
        for (int i = 0; i < nums.length - 1; i++) {
            if (nums[i] > nums[i + 1]) return i;
        }
        
        return nums.length - 1;
    }
}
```

### Time and Space Complexity

N = length of the array `nums`
- Time: `O(N)`
- Space: `O(1)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Longest%20Peak)