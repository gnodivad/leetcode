# 0283. Move Zeroes

## Approach 1: Two pointer with two pass
Define a pointer to keep track the last index that keep track non-zero value. Loop through the array and when we encountered non-zero value, just save it to that index of the array and increment it for next non-zero value. After the first loop, just fill in zero for the rest of array. For example, `[0, 2, 3, 0 ,5]` will become `[2, 3, 5, 0, 5]` after first loop and the pointer will point to zero which is on index 4 of the array.

```Java
class Solution {
    public void moveZeroes(int[] nums) {
        int lastNonZeroIndex = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != 0) {
                nums[lastNonZeroIndex++] = nums[i];
            }
        }
        
        for (int i = lastNonZeroIndex; i < nums.length; i++) {
            nums[i] = 0;
        }
    }
}
```

### Time and Space Complexity

N = The size of the array `nums`
- Time: `O(N)`
- Space: `O(1)`

## Approach 2: Two pointer with single pass
The approach 1 will have worse performance when the input is `[0,0,0,0,1]` because it always to `N` write operations. The better approach is just need to swap the `0` in index 0 and `1` in the last index.

```Java
class Solution {
    public void moveZeroes(int[] nums) {
        for (int lastNonZeroIndex = 0, curr = 0; curr < nums.length; curr++) {
            if (nums[curr] != 0) {
                int temp = nums[curr];
                nums[curr] = nums[lastNonZeroIndex];
                nums[lastNonZeroIndex++] = temp;
            }
        }
    }
}
```

### Time and Space Complexity

N = The size of the array `nums`
- Time: `O(N)`
- Space: `O(1)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Move%20Element%20To%20End)