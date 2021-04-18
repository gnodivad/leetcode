# 0701. Insert into a Binary Search Tree

## Approach 1
Add the val as a new node to the correct leaf node. Traverse to the leaf node by go to right subtree if the value is greater than current node value or go to left subtree if the value is less than current node value.

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
    public TreeNode insertIntoBST(TreeNode root, int val) {
        TreeNode currentNode = root;
        TreeNode newNode = new TreeNode(val);
        
        if (root == null) return newNode;
        
        while (true) {
            if (val < currentNode.val) {
                if (currentNode.left == null) {
                    currentNode.left = newNode;
                    break;
                } else {
                    currentNode = currentNode.left;
                }
            } else {
                if (currentNode.right == null) {
                    currentNode.right = newNode;
                    break;
                } else {
                    currentNode = currentNode.right;
                }
            }
        }
        
        return root;
    }
}
```

### Time and Space Complexity

H = height of the tree
- Time: `O(log(H))`
- Space: `O(1)`

## References
- None