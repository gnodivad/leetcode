# 0167. Two Sum II - Input array is sorted

## Approach 1: Two Pointers
We use two pointers that will pointing to first and last element in the array respectively. If the sum is equal to `target`, we found the exactly one solution. If it is less than `target`, move the pointer in smaller index from left to right. Otherwise move the pointer in larger index from right to left.

```Java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int left = 0, right = numbers.length - 1;
		
		while (left < right) {
			int currSum = numbers[left] + numbers[right];
			
			if (currSum == target) {
				return new int[]{left + 1, right + 1};
			} else if (currSum < target) {
				left++;
			} else {
				right--;
			}
		}
		
        return new int[0];
    }
}
```

### Time and Space Complexity

N = size of the numbers array
- Time: `O(N)`
- Space: `O(1)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Two%20Number%20Sum)