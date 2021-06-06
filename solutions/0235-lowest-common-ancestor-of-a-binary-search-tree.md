# 0235. Lowest Common Ancestor of a Binary Search Tree

## Approach 1
The condition to become LCA for two node are the LCA node must be greater than left node and smaller than right node. If both left and right node is greater than current node, we can conclude than LCA is on the right subtree. Otherwise, we should search on left subtree.

```Java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        TreeNode parent = root;
        
        while (parent != null) {
            if (p.val > parent.val && q.val > parent.val) {
                parent = parent.right;
            } else if (p.val < parent.val && q.val < parent.val) {
                parent = parent.left;
            } else {
                return parent;
            }
        }
        
        return null;
    }
}
```

### Time and Space Complexity

N = Total of the node in the tree `root`
- Time: `O(N)`
- Space: `O(1)`

## References
- EPI 15.4