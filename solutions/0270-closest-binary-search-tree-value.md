# 0270. Closest Binary Search Tree Value

## Approach 1: Recursive
Recursively call to find closest value by pass in `closest` as the current closest value in Binary Tree. The node of the tree will become `closest` if the different of the value is smaller than the difference of `closest` with `target`. If `target` is greater than current node value, move to the right of the node. Otherwise, move to the right.

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
    public int closestValue(TreeNode root, double target) {
        return closestValue(root, target, root.val);
    }
    
    public int closestValue(TreeNode tree, double target, int closest) {
		if (tree == null) return closest;
		
		if (Math.abs(target - closest) > Math.abs(target - tree.val)) {
			closest = tree.val;
		}
		
		if (tree.val == target) {
			return closest;
		} else if  (tree.val < target) {
			return closestValue(tree.right, target, closest);
		} else {
			return closestValue(tree.left, target, closest);
		}
	}
}
```

### Time and Space Complexity

k = height of binary tree
- Time: `O(log(h))`
- Space: `O(log(h))`



## References
- [AlgoExpert](https://www.algoexpert.io/questions/Find%20Closest%20Value%20In%20BST)