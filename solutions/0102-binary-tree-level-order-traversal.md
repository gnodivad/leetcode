# 0102. Binary Tree Level Order Traversal

## Approach 1: Breadth-first Search
Use BFS to traverse through the tree with add the root into the queue. While the queue is not empty, adding an empty list into result array `results`  and compute how many elements on the current level. Pop out all these elements from the queue and add them into correct array in `results` and add their child nodes into queue for the next level.

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> results = new ArrayList<>();
        
        if (root == null) return results;
        
        Deque<TreeNode> queue = new LinkedList<TreeNode>();
        queue.addLast(root);
        
        int height = 0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            
            results.add(new ArrayList<>());
            
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.removeFirst();
                
                results.get(height).add(node.val);
                
                if (node.left != null) {
                    queue.addLast(node.left);
                }
                
                if (node.right != null) {
                    queue.addLast(node.right);
                }
            }
            
            height++;
        }
        
        return results;
    }
}
```

### Time and Space Complexity

N = total number of node in the tree
- Time: `O(N)`
- Space: `O(N)`

## References
- EPI 9.7