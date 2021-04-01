# 0145. Binary Tree Postorder Traversal

## Approach 1: Recursive
Use recursion to traversal all the nodes of the tree go to the left child of the node,then go to the right child and then just add the nodes value to the output array.

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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> array = new ArrayList<>();
        postorderTraversal(root, array);
        return array;
    }
    
    public void postorderTraversal(TreeNode node, List<Integer> array) {
        if (node == null) return;

        postorderTraversal(node.left, array);
        postorderTraversal(node.right, array);
        array.add(node.val);
    }
}
```

### Time and Space Complexity

N = total number of node in the tree
- Time: `O(N)`
- Space: `O(log(N)) to O(N)`
	- Average case is `log(N)` if the tree is balanced
	- `O(N)` when tree is unbalanced in the way of all nodes either have only left child or right child

## References
- [AlgoExpert](https://www.algoexpert.io/questions/BST%20Traversal)