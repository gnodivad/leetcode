# 0746. Min Cost Climbing Stairs

## Approach 1: Bottom-Up
Since we can take 1 or 2 steps at a time, and pay the respective cost to continue. Let look at an example `costs = [0,1,2,3,4,5]`. We need to reach either step 4 or step 5 before each the top. The minimum cost to reach to top is defined as `minimumCost[6] = min(4 + minimumCost[4], 5 + minimumCost[5])`.

```Java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int[] minimumCost = new int[cost.length + 1];
        
        for (int i = 2; i <= cost.length; i++) {
            minimumCost[i] = Math.min(minimumCost[i - 2] + cost[i - 2], minimumCost[i - 1] + cost[i - 1]);
        }
        
        return minimumCost[minimumCost.length - 1];
    }
}
```

### Time and Space Complexity

N = length of the array `cost`
- Time: `O(N)`
- Space: `O(N)`

## Approach 2: Bottom-Up with constant space
From approach 1, we know that we only cares about 2 steps below current step. Initialize two variables, `downOne` and `downTwo`, that represent the minimum cost to reach one step and two step below the current step. At each iteration, we simulate moving 1 step up by assuming `downOne` as current step and the store the minimum cost to reach current step at current index. The minimum cost to reach here is the minimum value between `downTwo + cost[i - 2]` and `downOne + cost[i - 1]`. After that, `downTwo` will be update to whatever `downOne` was prior to the update.

```Java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int downOne = 0;
        int downTwo = 0;
        
        for (int i = 2; i <= cost.length; i++) {
            int temp = downOne;
            downOne = Math.min(downTwo + cost[i - 2], downOne + cost[i - 1]);
            downTwo = temp;
        }
        
        return downOne;
    }
}
```

### Time and Space Complexity

N = length of the array `cost`
- Time: `O(N)`
- Space: `O(1)`

## References
- None