# 0287. Find the Duplicate Number

## Approach 1: HashSet
Use HashSet to keep track all the numbers has found so far. Return the value if the value exists in HashSet before add it.

```Java
class Solution {
    public int findDuplicate(int[] nums) {
        HashSet<Integer> set = new HashSet();
		
		for (int num : nums) {
			if (set.contains(num)) {
				return num;
			}
			
			set.add(num);
		}
		
        return -1;
    }
}
```

### Time and Space Complexity

N = length of the array `nums`
- Time: `O(N)`
- Space: `O(N)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/First%20Duplicate%20Value)