# 0845. Longest Mountain in Array

## Approach 1
Go through all elements in `arr` to find the peak, which the element that will greater than both of it's neighbour. When we found it, just expand the search boundary to the left and right. The left boundary will always expand when the element have smaller value than its right neighbour. The right boundary will always expand when the element have smaller value than its left neighbour.

```Java
class Solution {
    public int longestMountain(int[] arr) {
        int maxPeak = 0;
        
        for (int i = 1; i < arr.length - 1; i++) {
            boolean isPeak = arr[i] > arr[i - 1] && arr[i] > arr[i + 1];
            
            if (!isPeak) continue;
            
            int count = 1;
            for (int leftIdx = i - 1; leftIdx >= 0; leftIdx--) {
                if (arr[leftIdx] >= arr[leftIdx + 1]) break;
                
                count++;
            }
            
            for (int rightIdx = i + 1; rightIdx < arr.length; rightIdx++) {
                if (arr[rightIdx] >= arr[rightIdx - 1]) break;
                
                count++;
            }
            
            maxPeak = Math.max(count, maxPeak);
        }
        
        return maxPeak;
    }
}
```

### Time and Space Complexity

N = length of the array `arr`
- Time: `O(N)`
- Space: `O(1)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Longest%20Peak)