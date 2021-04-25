# 0110. Balanced Binary Tree

## Approach 1
Defined an global variable `isBalancedTree` and set it to true to assume that every tree is balanced tree at first. Traverse the tree and calculate the height of left and right subtree for each of the node. If the node is the leaf node, the height of its both subtree is `0`. Otherwise, we should return the maximum height between left subtree and right tree plus 1 to the parent.

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
    public boolean isBalancedTree;
    
    public boolean isBalanced(TreeNode root) {
        isBalancedTree = true;
		
		traverseTree(root);
		
        return isBalancedTree;
    }
    
    public int traverseTree(TreeNode tree) {
		if (tree == null) return 0;
		
		int leftSubtreeHeight = traverseTree(tree.left);
		int rightSubtreeHeight = traverseTree(tree.right);
		
		if (Math.abs(leftSubtreeHeight - rightSubtreeHeight) > 1) {
			isBalancedTree = false;
		}
		
		return 1 + Math.max(leftSubtreeHeight, rightSubtreeHeight);
	}
}
```

### Time and Space Complexity

N = number of node in the tree
- Time: `O(N)`
- Space: `O(N)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Height%20Balanced%20Binary%20Tree)