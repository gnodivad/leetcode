# 0021. Merge Two Sorted Lists

## Approach 1: Two Pass
Initial `prehead` and `tail` points to a dummy node and build up the next node by comparing the first node from both linked list iteratively.

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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode prehead = new ListNode(-1);
        ListNode tail = prehead;
        
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                tail.next = l1;
                l1 = l1.next;
            } else {
                tail.next = l2;
                l2 = l2.next;
            }
            tail = tail.next;
        }
        
        tail.next = l1 == null ? l2 : l1;
        
        return prehead.next;
    }
}
```

### Time and Space Complexity

L1 = Length of l1, L2 = Length of l2
- Time: `O(Max(L1, L2))`
- Space: `O(1)`

## References
- None