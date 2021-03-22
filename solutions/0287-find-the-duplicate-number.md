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

## Approach 2
Since the integer in the array will in the range `[1, n]` inclusive, it means that each position in the array should not contains more than two elements. For example, integer `1` should belongs to index `0` and integer `n` belongs to index `[n -1]` in the array. When we loop through the arrays, we can map the current integer to the index in array and mark it as negative to represent it this index is visited before. By repeat this process, if we find an index have negative value, we can ensure that integer that belongs to this index is the duplicate value.

```Java
class Solution {
    public int findDuplicate(int[] nums) {		
		for (int num : nums) {
			num = Math.abs(num);
            
            if (nums[num - 1] < 0) return num;
            
            nums[num - 1] *= -1;
		}
		
        return -1;
    }
}
```

### Time and Space Complexity

N = length of the array `nums`
- Time: `O(N)`
- Space: `O(1)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/First%20Duplicate%20Value)