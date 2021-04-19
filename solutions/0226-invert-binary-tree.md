# 0226. Invert Binary Tree

## Idea
For each node, we just need to swap the left subtree and right subtree from root to leaf node.

## Approach 1
Use stack to traverse the tree and perform the swapping action.

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
    public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        
        Deque<TreeNode> stack = new LinkedList<>();
		stack.push(root);
		
		while(!stack.isEmpty()) {
			TreeNode currentNode = stack.pop();
			
			TreeNode tempLeftNode = currentNode.left;
			currentNode.left = currentNode.right;
			currentNode.right = tempLeftNode;
			
			if (currentNode.left != null) {
				stack.push(currentNode.left);
			}
			
			if (currentNode.right != null) {
				stack.push(currentNode.right);
			}
		}
        
        return root;
    }
}
```

### Time and Space Complexity

N = total of node in the tree
- Time: `O(N)`
- Space: `O(N)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Invert%20Binary%20Tree)