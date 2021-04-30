# 0104. Maximum Depth of Binary Tree

## Approach 1
Maximum depth defined as the maximum number of steps to reach a leaf node from root node. For every node, we pass to parent node the value of `maximum depth for left subtree and right subtree + 1`. 

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
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        
        int leftDepth = maxDepth(root.left);
        int rightDepth = maxDepth(root.right);
        
        return 1 + Math.max(leftDepth, rightDepth);
    }
}
```

### Time and Space Complexity

N = total number of node in the tree
- Time: `O(N)`
- Space: `O(Log(N))`

## References
- None