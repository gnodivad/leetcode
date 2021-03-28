# 0098. Validate Binary Search Tree

## Approach 1
Compare each node value with upper and lower limits been specify when traverse from the root. When traverse to the left child, the upper will be bounds by the parent and lower will remains by following parent's lower bounds. However if traverse to the right child, the lower will be bounds by the parent in this case and upper will remains the same. By having upper and lower bounds limit, we able to check each node is stay within the limit.

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
    public boolean isValidBST(TreeNode root) {
        return isValidBST(root, null, null);
    }
    
    public boolean isValidBST(TreeNode node, Integer lower, Integer upper) {
        if (node == null) return true;
        
        if ((lower != null && lower >= node.val) || (upper != null && node.val >= upper)) return false;
        
        return isValidBST(node.left, lower, node.val) && isValidBST(node.right, node.val, upper);
    }
}
```

### Time and Space Complexity

N = total number of node in the tree, H = height of the tree
- Time: `O(N)`
- Space: `O(H)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Validate%20BST)