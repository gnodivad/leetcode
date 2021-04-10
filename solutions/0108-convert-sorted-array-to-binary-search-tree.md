# 0108. Convert Sorted Array to Binary Search Tree

## Approach 1
Implemented helper function to take in extra two params `fromIndex` and `toIndex` for construct BST from element between that two specific index in the array. Everytime, we create new node with the middle element in the array. Left child and right child of it will construct from the `fromIndex` to middle element and middle element to `toIndex` respectively.

```Java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        return sortedArrayToBST(nums, 0, nums.length - 1);
    }
    
    public TreeNode sortedArrayToBST(int[] nums, int fromIndex, int toIndex) {
        if (fromIndex > toIndex) return null;
        
        int middle = fromIndex + (toIndex - fromIndex) / 2;
        TreeNode node = new TreeNode(nums[middle]);
        node.left = sortedArrayToBST(nums, fromIndex, middle - 1);
        node.right = sortedArrayToBST(nums, middle + 1, toIndex);
        
        return node;
    }
}
```

### Time and Space Complexity

N = total number of node in the tree
- Time: `O(N)`
- Space: `O(Log(N))`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Validate%20BST)