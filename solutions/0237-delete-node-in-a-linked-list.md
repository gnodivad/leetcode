# 0237. Delete Node in a Linked List

## Approach 1
Copy the next node val to current node and point the next pointer to what next node points to.

```Java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public void deleteNode(ListNode node) {
        node.val = node.next.val;
        node.next = node.next.next;
    }
}
```

### Time and Space Complexity

- Time: `O(1)`
- Space: `O(1)`

## References
- None