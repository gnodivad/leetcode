# 0230. Kth Smallest Element in a BST

## Approach 1
Traverse the binary tree in ascending order by using inorder strategy. When traversing the tree, we need to keep track how many node we been visited `totalOfNodeVisited` and what is the latest node value that we visited `latestNodeValue`. We update both value when the `totalOfNodeVisited` is less than `k` and continue to traverse to other node.

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
    public class TreeInfo {
        public int totalOfNodeVisited;
        public int latestNodeValue;
        
        public TreeInfo(int totalOfNodeVisited, int latestNodeValue) {
            this.totalOfNodeVisited = totalOfNodeVisited;
            this.latestNodeValue = latestNodeValue;
        }
    }
    
    public int kthSmallest(TreeNode root, int k) {
        TreeInfo treeInfo = new TreeInfo(0, -1);
        traverseTree(root, k, treeInfo);
        return treeInfo.latestNodeValue;
    }
    
    public void traverseTree(TreeNode node, int k, TreeInfo treeInfo) {
        if (node == null || treeInfo.totalOfNodeVisited >= k) return;
        
        traverseTree(node.left, k, treeInfo);
        if (treeInfo.totalOfNodeVisited < k) {
            treeInfo.totalOfNodeVisited += 1;
            treeInfo.latestNodeValue = node.val;
            traverseTree(node.right, k, treeInfo);
        }
    }
}
```

### Time and Space Complexity

H = height of the tree `node`
- Time: `O(H)`
- Space: `O(log(H)) to O(H)`
	- Average case is `log(H)` if the tree is balanced
	- `O(H)` when tree is unbalanced in the way of all nodes either have only left child or right child

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Find%20Kth%20Largest%20Value%20In%20BST)