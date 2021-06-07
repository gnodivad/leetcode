# 0134. Gas Station

## Approach 1: One Pass
Iterate through all the gas station and sum up all the refuel gas and cost taken to move to next station `totalTank = sum(gas[0...n]) - sum(cost[0...n])`. During this process, we should find the gas station that have the minimum value of `totalTank`. The gas comsumption is the same no matter which gas station we begin from. So, we just start from the gas station which have the minimum value of `totalTank`, we will complete the journey if the `totalTank` is never result in negative value after we iterate through all the gas station.

```Java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int gasStation = 0;
        
        int totalTank = 0;
        int minimumTank = Integer.MAX_VALUE;
    
        for (int i = 0; i < gas.length; i++) {
            totalTank += (gas[i] - cost[i]);
            
            if (totalTank < minimumTank) {
                gasStation = i;
                minimumTank = totalTank;
            }
        }
        
        return totalTank >= 0 ? (gasStation + 1) % gas.length : -1;
    }
}
```

### Time and Space Complexity

N = Total of the gas station
- Time: `O(N)`
- Space: `O(1)`

## References
- EPI 18.6