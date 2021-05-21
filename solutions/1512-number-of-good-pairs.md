# 1512. Number of Good Pairs

## Approach 1: Iteration
Use a HashMap to keep track the num. The total of good pair should be increment by the total of times num recorded in the HashMap previously, because the current number can form good pair with each of them.

```Java
class Solution {
    public int numIdenticalPairs(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<>();
        
        int total = 0;
        for (int num : nums) {
            if (map.containsKey(num)) {
                total += map.get(num);
            }
            
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        
        return total;
    }
}
```

### Time and Space Complexity

N = length of the array `nums`, M = length of unique number in the array `nums`
- Time: `O(N)`
- Space: `O(M)`

## References
- None