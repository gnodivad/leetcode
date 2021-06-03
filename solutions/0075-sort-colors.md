# 0075. Sort Colors

## Approach 1: One Pass
Initialize pointer `smaller = 0` for lower boundary, `current = 0`, and `larger = nums.length - 1` for upper boundary. Repeat the following step until `current === larger`
- `nums[current]` is lowest value `0`, swap with any nums in `nums[smaller]`. Increment `current` and `smaller`.
- `nums[current]` is highest value `2`, swap with any nums in `nums[larger]`. Decrement `larger`.
- `nums[current]` is `1`. Since it is in correct position, increment `current`.

```Java
class Solution {
    public void sortColors(int[] nums) {
        int smaller = 0, current = 0, larger = nums.length - 1;
        
        int temp;
        while (current <= larger) {
            if (nums[current] == 0) {
                temp = nums[smaller];
                nums[smaller++] = nums[current];
                nums[current++] = temp;
            } else if (nums[current] == 2) {
                temp = nums[larger];
                nums[larger--] = nums[current];
                nums[current] = temp;
            } else {
                current++;
            }
        }
    }
}
```

### Time and Space Complexity

N = The length of array `nums`
- Time: `O(N)`
- Space: `O(1)`

## References
- EPI 6.1