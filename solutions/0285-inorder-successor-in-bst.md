# 0285. Inorder Successor in BST

## Approach 1
If the right child exists, we can find the leftmost node in the right subtree of that node. Otherwise, we can run the inorder traversal on the root node and everytime we update the current node as `previousNode` before we continue the inorder traversal. During the next recursive call, we can check if the `previousNode` is equal to our target node. If that is the case, it meants that `previousNode` is the predecessor of current node and current node is the successor of the previous node.

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
    private TreeNode previousNode;
    private TreeNode inorderSuccessorNode;
    
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        if (p.right != null) {
            TreeNode current = p.right;
            while (current.left != null) current = current.left;
            inorderSuccessorNode = current;
        } else {
            inorderTraverse(root, p);
        }
        
        return inorderSuccessorNode;
    }
    
    public void inorderTraverse(TreeNode node, TreeNode p) {
        if (node == null) return;
        
        inorderTraverse(node.left, p);
        
        if (previousNode == p && inorderSuccessorNode == null) {
            inorderSuccessorNode = node;
        }
        
        previousNode = node;
        inorderTraverse(node.right, p);
    }
}
```

### Time and Space Complexity

N = The total number of node in tree
- Time: `O(N)`
- Space: `O(N)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Find%20Successor)