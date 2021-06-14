# 0101. Symmetric Tree

## Approach 1: BFS
Everytime, each two consecutive nodes in the queue should be equal and their subtrees should be a mirror of each other. Initially, the queue contains `root.left` as `t1` and `root.right` as `t2`. Each time, two nodes are extracted and their values compared `t1.val == t2.val`. The children of the two nodes are inserted in the queue in the correct order such that `t1.left` will compared with `t2.right` and `t1.right` will compared with `t2.left`.

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
    public boolean isSymmetric(TreeNode root) {
        if (root == null) return true;
        
        Deque<TreeNode> queue = new LinkedList<>();
        queue.add(root.left);
        queue.add(root.right);
        
        while (!queue.isEmpty()) {
            TreeNode t1 = queue.poll();
            TreeNode t2 = queue.poll();
            
            if (t1 == null && t2 == null) continue;
            if (t1 == null || t2 == null) return false;
            if (t1.val != t2.val) return false;
            queue.add(t1.left);
            queue.add(t2.right);
            queue.add(t1.right);
            queue.add(t2.left);
        }
        
        return true;
    }
}
```

### Time and Space Complexity

N = total number of node in the tree, H = height of the tree
- Time: `O(N)`
- Space: `O(H)`

## References
- EPI 10.2