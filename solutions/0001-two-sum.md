# 0001. Two Sum

## Approach 1: Hash Table
We iterate all the numbers in `num` and we do lookup to find the compliment. If it exists, we can return the result immediately. Otherwise, insert the elements into the hash table.

```Java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
		
		for (int i = 0; i < nums.length; i++) {
			if (map.containsKey(target - nums[i])) {
				return new int[]{i, map.get(target - nums[i])};
			}
			
			map.put(nums[i], i);
		}

        return new int[0];
    }
}
```

### Time and Space Complexity

- Time: `O(n)`
- Space: `O(n)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Two%20Number%20Sum)