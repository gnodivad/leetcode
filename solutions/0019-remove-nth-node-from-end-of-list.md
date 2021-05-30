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

## Approach 2: One Pass
Maintain two pointer, `fast` and `slow`. The distance between them should be `n` node. When `fast` pointer is null, the `slow` pointer will points to the node before the node that going to delete.

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
        
        ListNode fast = dummy;
        ListNode slow = dummy;
        for (int i = 0; i <= n; i++) {
            fast = fast.next;
        }
        
        while (fast != null) {
            fast = fast.next;
            slow = slow.next;
        }
        
        slow.next = slow.next.next;
        
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