# 0896. Monotonic Array

## Approach 1: One Pass
If an array is monotone increasing, the last element in the array must be larger or equal to first element. Otherwise, the last element will be smaller than first element. After we know the type of monotone, we can loop through all the elements in the array and check for is the element fullfill the type of monotone. For monotone increasing, `array[i] <= array[i + 1]`, and montone decreasing, `array[i] >= array[i + 1]`.

```Java
class Solution {
    public boolean isMonotonic(int[] array) {
        if (array.length <= 1) return true;
		
		boolean isIncreasing = array[array.length - 1] >= array[0] ? true : false;
		
		for (int i = 1; i < array.length; i++) {
			if (isIncreasing && array[i] < array[i - 1]) {
				return false;
			} else if (!isIncreasing && array[i] > array[i - 1]) {
				return false;
			}
		}
		
        return true;
    }
}
```

### Time and Space Complexity

N = length of the array `array`
- Time: `O(N)`
- Space: `O(1)`

## Approach 2: One Pass (Simple Variant)
For an array to be monotone, it is either be monotone increasing or monotone decreasing. First let us assume that array is monotone increasing and decreasing at the same time, and we perform checking for all the elements in the array. If we find the element `i` is greater than `i - 1`, then the array is concluded as not monotone decreasing anymore. If we find the element `i` is smaller than `i - 1`, then the array should not be monotone increasing.

```Java
class Solution {
    public boolean isMonotonic(int[] array) {
        boolean isIncreasing = true;
		boolean isDecreasing = true;
		
		for (int i = 1; i < array.length; i++) {
			if (array[i] > array[i - 1]) {
				isDecreasing = false;
			} else if (array[i] < array[i - 1]) {
				isIncreasing = false;
			}
		}
		
        return isIncreasing | isDecreasing;
    }
}
```

### Time and Space Complexity

N = length of the array `array`
- Time: `O(N)`
- Space: `O(1)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Monotonic%20Array)