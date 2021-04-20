# 0543. Diameter of Binary Tree

## Approach 1
The longest path has to be between two leaf nodes. For each node, the sum of the longest path of left subtree and right subtree might be the longest path in the tree. Besides that, the longest path of either left subtree or right subtree of that node might be part of the longest path in the tree.

Before we traverse the tree, we should mantain an variable `globalSum` to keep tracks of the longest path in the tree at that moment. Everytime we just compared the sum of the longest path of left subtree and right subtree with the `globalSum`, and update it if the larger value is encountered. Then, we just return the longest path either for left subtree or right subtree to the parent node.

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
    private int globalMax;
    
    public int diameterOfBinaryTree(TreeNode root) {
        globalMax = Integer.MIN_VALUE;
        
        traverseTree(root);
		
        return globalMax;
    }
    
    public int traverseTree(TreeNode tree) {
        if (tree == null) return 0;
		
		int totalMaxEdgeOnLeft = traverseTree(tree.left);
		int totalMaxEdgeOnRight = traverseTree(tree.right);
		
		globalMax = Math.max(globalMax, totalMaxEdgeOnLeft + totalMaxEdgeOnRight);
		
		return 1 + Math.max(totalMaxEdgeOnLeft, totalMaxEdgeOnRight);   
    }
}
```

### Time and Space Complexity
N = total of node in binary tree
- Time: `O(N)`
- Space: `O(N)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Binary%20Tree%20Diameter)