# 0144. Binary Tree Preorder Traversal

## Approach 1: Recursive
Use recursion to traversal all the nodes of the tree by add the root node to the array first, then go to the left child of the node,and then go to the right child.

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
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> array = new ArrayList<>();
        preorderTraversal(root, array);
        return array;
    }
    
    public void preorderTraversal(TreeNode node, List<Integer> array) {
        if (node == null) return;
        
        array.add(node.val);
        preorderTraversal(node.left, array);
        preorderTraversal(node.right, array);
    }
}
```

### Time and Space Complexity

N = total number of node in the tree
- Time: `O(N)`
- Space: `O(log(N)) to O(N)`
	- Average case is `log(N)` if the tree is balanced
	- `O(N)` when tree is unbalanced in the way of all nodes either have only left child or right child

## Approach 2: Morris Travesal
Use Morris Traversal to traverse all the nodes in tree. Morris Traversal will always append the right subtree to the rightmost node in the left subtree. In the end, the tree will only have right child only for each of the node.

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
    public List<Integer> preorderTraversal(TreeNode root) {
        LinkedList<Integer> output = new LinkedList<>();
        
        TreeNode curr = root;
        TreeNode pre;
        
        while (curr != null) {
            if (curr.left == null) {
                output.add(curr.val);
                curr = curr.right;
            } else {
                pre = curr.left;
                while (pre.right != null) {
                    pre = pre.right;
                }
                
                output.add(curr.val);
                pre.right = curr.right;
                curr = curr.left;
            }
        }
        
        return output;
    }
}
```

### Time and Space Complexity

N = total number of node in the tree
- Time: `O(N)`
- Space: `O(1)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/BST%20Traversal)