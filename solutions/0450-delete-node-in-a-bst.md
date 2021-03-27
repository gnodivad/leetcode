# 0450. Delete Node in a BST

## Approach 1: Recursion
Three possible situation will happen during deletion:
- The node is a left, and we could delete it straighaway.
- The node is not a leaf, and it has a right child. The node could be replaced by its successor, which is the smallest node after the node that going to delete. After that, we can delete the successor node from the right tree of current node.
- THe node is not a leaf, and it has a left child. The node could be replaced by its predecessor, which is the largest node before the node that going to delete. After that, we can the predecessor node from the left tree of current node.

```java
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
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) return null;
        
        if (key > root.val) root.right = deleteNode(root.right, key);
        else if (key < root.val) root.left = deleteNode(root.left, key);
        else {
            if (root.left == null && root.right == null) {
                root = null;
            } else if (root.right != null) {
                root.val = successor(root);
                root.right = deleteNode(root.right, root.val);
            } else {
                root.val = predecessor(root);
                root.left = deleteNode(root.left, root.val);
            }
        }
        
        return root;
    }
    
    public int successor(TreeNode node) {
        node = node.right;
        
        while (node.left != null) {
            node = node.left;
        }
        
        return node.val;
    }
    
    public int predecessor(TreeNode node) {
        node = node.left;
        
        while (node.right != null) {
            node = node.right;
        }
        
        return node.val;
    }
}
```

### Time and Space Complexity
N = Total number of node in the tree, H = Height of the tree
- Time: `O(log2(N))`
- Space: `O(H)` for the recursion stack.

## References
- [AlgoExpert](https://www.algoexpert.io/questions/BST%20Construction)