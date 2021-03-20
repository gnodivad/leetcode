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

## Approach 2: Iterative Binary Search
We can apply the binary search to find the peak. By always element in the middle and the right element next to it, we will know the current element is in increasing slope or decreasing slope. When in increasing slope, we know the peak will exist in the right side of the middle element. Otherwise, it will exist in the left side of the middle element.

```Java
class Solution {
    public int findPeakElement(int[] nums) {        
        int left = 0, right = nums.length - 1;
        
        while (left < right) {
            int mid = (left + right) / 2;
            
            if (nums[mid] > nums[mid + 1]) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        
        return left;
    }
}
```

### Time and Space Complexity

N = length of the array `nums`
- Time: `O(log2(N))`
- Space: `O(1)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Longest%20Peak)