# 1200. Minimum Absolute Difference

## Approach 1: Sorting
Sort the array in ascending order and we can find the smallest difference of that element with the neighbour element in the array. If the difference of two element is same as before, we just append the pairs into the output array. Otherwise if the difference is smaller than before, initialise a new output array.

```Java
class Solution {
    public List<List<Integer>> minimumAbsDifference(int[] arr) {
        Arrays.sort(arr);
        
        List<List<Integer>> results = new ArrayList<>();
        
        int min = Integer.MAX_VALUE;
        
        for (int i = 1; i < arr.length; i++) {
            int diff = Math.abs(arr[i] - arr[i - 1]);
            if (diff < min) {
                min = diff;
                results = new ArrayList<>();
                results.add(Arrays.asList(arr[i - 1], arr[i]));
            } else if (diff == min) {
                results.add(Arrays.asList(arr[i - 1], arr[i]));
            }
        }
        
        return results;
    }
}
```

### Time and Space Complexity

N = length of the array `arr`
- Time: `O(Nlog(N))`
- Space: `O(1)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Smallest%20Difference)