# 0083. Remove Duplicates from Sorted List

## Approach 1
Go through every node in the linked list, find the next distinct element for every node, and link them after current node.

```Java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode currentNode = head;
        
        while (currentNode != null) {
            ListNode nextDistinctNode = currentNode;
            
            while (nextDistinctNode != null && nextDistinctNode.val == currentNode.val) {
                nextDistinctNode = nextDistinctNode.next;
            }
            
            currentNode.next = nextDistinctNode;
            currentNode = nextDistinctNode;
        }
        
        return head;
    }
}
```

### Time and Space Complexity

N = total number of node in linked list
- Time: `O(N)`
- Space: `O(1)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Remove%20Duplicates%20From%20Linked%20List)