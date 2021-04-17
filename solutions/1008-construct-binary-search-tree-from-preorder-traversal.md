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

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Reconstruct%20BST)