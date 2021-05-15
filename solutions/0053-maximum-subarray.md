# 0054. Spiral Matrix

## Approach 1: Kadane Algorithm
Any subarray whose sum is positive is probably is maximum subarray. Iterate through the input and keep track with two value, `currentMax` and `globalMax`. When in index `i`, if the `currentMax + nums[i]` is less than `nums[i]`, it meant that we can give up the maximum subarray that we found in previous index and update it to `nums[i]`. Update `globalMax` if the `currentMax` has greater value.

```Java
class Solution {
    public int maxSubArray(int[] nums) {
        int currentMax = nums[0];
		int globalMax = nums[0];
		
		for (int i = 1; i < nums.length; i++) {
			currentMax = Math.max(nums[i], nums[i] + currentMax);
			if (currentMax > globalMax) {
				globalMax = currentMax;
			}
		}
		
        return globalMax;
    }
}
```

### Time and Space Complexity

N = length of array `nums`
- Time: `O(N)`
- Space: `O(1)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Kadane's%20Algorithm)