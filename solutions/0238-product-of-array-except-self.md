# 0238. Product of Array Except Self

## Approach 1
The total product for each element at index `i` is the multiplication of total product to the left of the element and total product to the right of the element. Loop throught nums 2 times to compute the product from left to right and right to left except self. The first loop will calculate the total product to the left of the element, and element index `0` will have value 1 since there are no elements to the left. The other loop will do the inverse and last element will have value 1 since there are no elements to the right. However, the only change in the second loop is we don't explicitly build the array by getting the total product to the right of element, we also need to updating the current index with the result that get in the first loop.

```Java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int[] results = new int[nums.length];
        
        int leftRunningProduct = 1;
        for (int i = 0; i < nums.length; i++) {
            results[i] = leftRunningProduct;
            leftRunningProduct *= nums[i];
        }
        
        int rightRunningProduct = 1;
        for (int i = nums.length - 1; i >= 0; i--) {
            results[i] *= rightRunningProduct;
            rightRunningProduct *= nums[i];
        }
        
        return results;
    }
}
```

### Time and Space Complexity

N = length of the array `nums`
- Time: `O(N)`
- Space: `O(1)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Array%20Of%20Products)