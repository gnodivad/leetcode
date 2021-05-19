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

## Approach 2: Divide and Conquer
When we split the input into half, the maximum subarray either:
- Uses elements only from left side
- Uses elements only from right side
- Combination from both side
The first and second case will be cover by when we split the input more. The current iteration will covered the third case. Since the subarray is combination from both side, we must the middle element. For current iteration, we can find the maximum sum for both by iterate to the beginning of left subarray and the end of right array from the middle. After that, we will can the maximum subarray for this set of input by the combination of `bestLeftSum + bestRightSum + array[middle]`.

```Java
class Solution {
    private int[] numsArray;
    
    public int maxSubArray(int[] nums) {
        numsArray = nums;
        
        return findBestSubarray(0, numsArray.length - 1);
    }
    
    private int findBestSubarray(int left, int right) {
        if (left > right) {
            return Integer.MIN_VALUE;
        }
        
        int mid = Math.floorDiv(left + right, 2);
        int curr = 0;
        int bestLeftSum = 0;
        int bestRightSum = 0;
        
        for (int i = mid - 1; i >= left; i--) {
            curr += numsArray[i];
            bestLeftSum = Math.max(bestLeftSum, curr);
        }
        
        curr = 0;
        for (int i = mid + 1; i <= right; i++) {
            curr += numsArray[i];
            bestRightSum = Math.max(bestRightSum, curr);
        }
        
        int bestCombinedSum = numsArray[mid] + bestLeftSum + bestRightSum;
        
        int leftHalf = findBestSubarray(left, mid - 1);
        int rightHalf = findBestSubarray(mid + 1, right);
        
        return Math.max(bestCombinedSum, Math.max(leftHalf, rightHalf));
    }
}
```

### Time and Space Complexity

N = length of array `nums`
- Time: `O(NLog(N))`
- Space: `O(Log(N))`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Kadane's%20Algorithm)