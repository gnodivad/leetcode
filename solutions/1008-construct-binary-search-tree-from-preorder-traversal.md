# 1008. Construct Binary Search Tree from Preorder Traversal

## Basic Idea
The preorder traversal will print out the node value first, then all the node value in left subtree and then all the node value in right subtree. By knowing this, we can conclude that the first element in the preorder array will always be the root. The problem is how we differentiate the left subtree and right subtree value for that root value.

## Approach 1
We just need to find the index of a value in the array that is greater than the node value. The element after that index will be all the value for right subtree and the element before that exclude the first element will be all the value of left subtree.

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
    public TreeNode bstFromPreorder(int[] preorder) {
        if (preorder.length == 0) return null;
        
        int currentValue = preorder[0];
        int rightTreeIndex = preorder.length;
        
        for (int i = 1; i < preorder.length; i++) {
            if (preorder[i] >= currentValue) {
                rightTreeIndex = i;
                break;
            }
        }
        
        TreeNode node = new TreeNode(currentValue);
        node.left = bstFromPreorder(Arrays.copyOfRange(preorder, 1, rightTreeIndex));
        node.right = bstFromPreorder(Arrays.copyOfRange(preorder, rightTreeIndex, preorder.length));
        
        return node;
    }
}
```

### Time and Space Complexity

N = the length of the array `preorder`, H = the height of the construct binary tree
- Time: `O(N^2)`
    - `O(N)` to go through all the element in the array `preorder`
    - `O(N)` to go through the array again to find the correct subarray for left and right subtree.
- Space: `O(H)`

## Approach 2
Since it is preorder traversal array, the element from left to right in the array will become root node when construct BST in sequence. We can use `rootIdx` to keep track the current node, and can avoid to construct subarray for left and right subtree like Approach 1. This approach, we will use specify two variable to keep track the lower and upper bound limit for the node. If we construct the left subtree, the lower bound will follow parent node's lower bound but upper bound will constraint by parent node value. The upper bound will remains the same as parent node's upper bound but lower bound will constraint by parent node value.

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
    TreeInfo treeInfo;
    
    public class TreeInfo {
        public int rootIdx;
        
        public TreeInfo(int rootIdx) {
            this.rootIdx = rootIdx;
        }
    }
    
    public TreeNode bstFromPreorder(int[] preorder) {
        this.treeInfo = new TreeInfo(0);
        
        return bstFromPreorderInRange(preorder, Integer.MIN_VALUE, Integer.MAX_VALUE);
    }
    
    public TreeNode bstFromPreorderInRange(int[] preorder, int lowerBound, int upperBound) {
        if (this.treeInfo.rootIdx == preorder.length) return null;
        
        int currentValue = preorder[this.treeInfo.rootIdx];
        if (currentValue < lowerBound || currentValue >= upperBound) return null;
        
        this.treeInfo.rootIdx++;
        TreeNode node = new TreeNode(currentValue);
        node.left = bstFromPreorderInRange(preorder, lowerBound, currentValue);
        node.right = bstFromPreorderInRange(preorder, currentValue, upperBound);
        
        return node;
    }
}
```

### Time and Space Complexity

N = the length of the array `preorder`, H = the height of the construct binary tree
- Time: `O(N)`
- Space: `O(H)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Reconstruct%20BST)