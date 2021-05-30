# 0019. Remove Nth Node From End of List

## Approach 1: Two Pass
Iterate through linked list to calculate the length of the linked list. After that, we can calculate the total move we going to move until the node before the deleted node.

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        
        int length = 0;
        ListNode current = head;
        
        while (current != null) {
            length++;
            current = current.next;
        }
        
        length -= n;
        current = dummy;
        while (length > 0) {
            length--;
            current = current.next;
        }
        
        current.next = current.next.next;
        
        return dummy.next;
    }
}
```

### Time and Space Complexity

N = length of the Linked List
- Time: `O(N)`
- Space: `O(1)`

## References
- None