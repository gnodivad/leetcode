# 0112. Path Sum

## Approach 1: Recursion
Going through the tree from root to leaf, each time will substract the node value from the target sum. Everytime when reach a leaf node in the tree, check the target sum is 0.

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
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if (root == null) return false;
        
        targetSum -= root.val;
        if (targetSum == 0 && root.left == null && root.right == null) {
            return true;
        }
        
        return hasPathSum(root.left, targetSum) || hasPathSum(root.right, targetSum);
    }
}
```

### Time and Space Complexity

N = number of node in the tree
- Time: `O(N)`
- Space: `O(N) to O(log(N))`
	- `O(N)` when the tree is unbalanced such as each node have one child node only.
	- `O(log(N))` when the tree is balanced

## Approach 2: Iteration
Create a class that associate an node and expected remaining sum from it's child node. Put the root into a stack and kickstart the interate process through the tree. Each time just remove a node from the top of the stack and check remaining sum is zero if it is a leaf node. Else, calculate the expected remaining sum for the child node and put them into the stack.

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
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if (root == null) return false;
        
        LinkedList<NodeWithRemainingSum> stack = new LinkedList();
        stack.add(new NodeWithRemainingSum(root, targetSum - root.val));
        
        while (!stack.isEmpty()) {
            NodeWithRemainingSum node = stack.removeFirst();
            
            if (node.remainingSum == 0 && 
                node.node.left == null && 
                node.node.right == null
               ) {
                return true;
            }
            
            if (node.node.left != null) {
                int remainingSum = node.remainingSum - node.node.left.val;
                stack.add(new NodeWithRemainingSum(node.node.left, remainingSum));
            }
            
            if (node.node.right != null) {
                int remainingSum = node.remainingSum - node.node.right.val;
                stack.add(new NodeWithRemainingSum(node.node.right, remainingSum));
            }
        }
        
        return false;
    }
}

class NodeWithRemainingSum {
    public TreeNode node;
    public int remainingSum;
    
    public NodeWithRemainingSum(TreeNode node, int remainingSum) {
        this.node = node;
        this.remainingSum = remainingSum;
    }
}
```

### Time and Space Complexity

N = number of node in the tree
- Time: `O(N)`
- Space: `O(N) to O(log(N))`
	- `O(N)` when the tree is unbalanced such as each node have one child node only.
	- `O(log(N))` when the tree is balanced

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Branch%20Sums)