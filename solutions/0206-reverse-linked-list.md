# 0206. Reverse Linked List

## Approach 1: Iterative
Create a pointer called `tail` and it always points to the head of the reverse linked list. Everytime we advance `head` to the next node, the previous node should become the first node that `tail` points to.

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
    public ListNode reverseList(ListNode head) {
        ListNode tail = null;
        
        while (head != null) {
            ListNode temp = head;
            head = head.next;
            temp.next = tail;
            tail = temp;
        }
        
        return tail;
    }
}
```

### Time and Space Complexity

N = The length of the linked list
- Time: `O(N)`
- Space: `O(1)`

## References
- None