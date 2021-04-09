# 0938. Range Sum of BST

## Idea
Since it is binary tree, we will know that all the left subtree of the node will be smaller than current node value and all the right subtree of node will be larger than current node. In this case, we can ignore the left subtree if current node value is equal to `low` and ignore the right subtree if current node value is equal to `high`.

## Approach 1: Recursion

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
    int sum;
    
    public int rangeSumBST(TreeNode root, int low, int high) {
        sum = 0;
        dfs(root, low, high);
        return sum;
    }
    
    public void dfs(TreeNode node, int low, int high) {
        if (node == null) return;
        
        if (low <= node.val && node.val <= high) {
            this.sum += node.val;
        }

        if (low < node.val) {
            dfs(node.left, low, high);            
        }
        
        if (high > node.val) {
            dfs(node.right, low, high);    
        }
    }
}
```

### Time and Space Complexity

N = number of nodes in the tree
- Time: `O(N)`
- Space: `O(N)`

## Approach 2: Interative

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
    public int rangeSumBST(TreeNode root, int low, int high) {
        int sum = 0;
        Deque<TreeNode> stack = new LinkedList<>();
        stack.push(root);
        
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            
            if (node == null) continue;
            
            if (low <= node.val && node.val <= high) {
                sum += node.val;
            }
            
            if (low < node.val) {
                stack.push(node.left);
            }
            
            if (node.val < high) {
                stack.push(node.right);
            }
        }
        
        return sum;
    }
}
```

### Time and Space Complexity

N = number of nodes in the tree
- Time: `O(N)`
- Space: `O(N)`

## References
- None