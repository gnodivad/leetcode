# 0198. House Robber

## Approach 1: Dynamic Programming
When reach to every house `houses`, we need to make the decision whether to go in or not. If entered previous house, we will not able to rob the current house. If we didn't entered previous house, we will able to rob this house. If there don't have any house, our profit will be zero and our profit will be the amount inside that house if there is only one house. If there is two house, the profit will be the maximum amount that either one of house have. The decision starting to get interesting when we have three house to rob. Let assume the profit that we able to rob from three houses as `robFrom(3)`, the amount that we able to get will be either just enter the house 1, or combine amount of house 1 and 2. The equation can be express as `robFrom(i) = max(robFrom(i - 1), robFrom(i - 2) + houses[i])`.

```Java
class Solution {
    public int rob(int[] nums) {
        if (nums.length == 0) return 0;
        if (nums.length == 1) return nums[0];
        
        int skipLastHouse = nums[0], skipNoHouse = Math.max(nums[0], nums[1]);
        
        for (int i = 2; i < nums.length; i++) {
            int current = Math.max(skipNoHouse, skipLastHouse + nums[i]);
            skipLastHouse = skipNoHouse;
            skipNoHouse = current;
        }
        
        return skipNoHouse;
    }
}
```

### Time and Space Complexity

N = size of the numbers array, `nums`
- Time: `O(N)`
- Space: `O(1)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Max%20Subset%20Sum%20No%20Adjacent)