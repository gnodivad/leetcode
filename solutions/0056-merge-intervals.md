# 0056. Merge Intervals

## Approach 1: Sorting
Sort the intervals by their `start` value, after that we just need to focus on `end` value. First, we use the first interval to determine that the next interval `start` is less than or equal to. If yes, we just need to alter the first interval `end` to the maximum `end` value between first interval and next interval. Otherwise, we can just append the interval to the `mergedInterval` since it does not intersect with next interval.

```Java
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        
        List<int[]> mergedInterval = new ArrayList<>();
        int[] currentInterval = intervals[0];
        
        for (int i = 1; i < intervals.length; i++) {
            if (intervals[i][0] > currentInterval[1]) {
                mergedInterval.add(currentInterval);
                currentInterval = intervals[i];
            } else {
                currentInterval[1] = Math.max(currentInterval[1], intervals[i][1]);
            }
        }
        
        mergedInterval.add(currentInterval);
        
        return mergedInterval.toArray(new int[mergedInterval.size()][]);
    }
}
```

### Time and Space Complexity

N = total number of elements in the input `matrix`
- Time: `O(NLog(N))`
- Space: `O(N)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Merge%20Overlapping%20Intervals)