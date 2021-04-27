# 1431. Kids With the Greatest Number of Candies

## Approach 1: Iteration
Find the maximum of candies the children have. For each children, calculate the total of candies again by assuming that all the `extraCandies` are belong to them. If the total is more than maximum, its meant that the children can have the greatest number of candles among them.

```Java
class Solution {
    public List<Boolean> kidsWithCandies(int[] candies, int extraCandies) {
        int max = candies[0];
        for (int i = 1; i < candies.length; i++) {
            max = Math.max(max, candies[i]);
        }
        
        List<Boolean> answer = new ArrayList<>();
        for (int i = 0; i < candies.length; i++) {
            answer.add(candies[i] + extraCandies >= max ? true : false);
        }
        
        return answer;
    }
}
```

### Time and Space Complexity

N = length of the array `candies`
- Time: `O(N)`
- Space: `O(1)`

## References
- None