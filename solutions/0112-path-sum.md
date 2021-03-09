# 0112. Path Sum

## Approach 1: Recursion
Going through the tree from root to leaf, each time will substract the node value from the target sum. Everytime when reach a leaf node in the tree, check the target sum is 0.

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
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if (root == null) return false;
        
        targetSum -= root.val;
        if (targetSum == 0 && root.left == null && root.right == null) {
            return true;
        }
        
        return hasPathSum(root.left, targetSum) || hasPathSum(root.right, targetSum);
    }
}
```

### Time and Space Complexity

N = number of node in the tree
- Time: `O(N)`
- Space: `O(N) to O(log(N))`
	- `O(N)` when the tree is unbalanced such as each node have one child node only.
	- `O(log(N))` when the tree is balanced

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Branch%20Sums)