# 0141. Linked List Cycle

## Approach 1: Floyd's Cycle Finding Algorithm
We can have two pointer to traverse linked list in different speed, `fast` and `slow`. `fast` will always move in 2 node and `slow` will move in 1 node. If the linked list don't have cycle, the `fast` pointer will reach the end of linked list first. Otherwise, `slow` pointer eventually will meet `fast` pointer in the cycle.

```Java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode fast = head, slow = head;
        
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            
            if (slow == fast) return true;
        }
        
        return false;
    }
}
```

### Time and Space Complexity

N = total number of nodes in the linked list
- Time: `O(N)`
    - `O(N)` when list has no cycle. Fast pointer must reach the end of the linked list to know that cycle is not exist.
    - `O(N)` when list has cycle. The distance between 2 runners at most the cyclic length `K`, for example 3 node that form the cycle will only have the maximum of distance `3`. If the speed difference between two runners is 1, then fast runner will take `3/1 = 3 loops` to catch up with slow runner. Besides that, we can confirm `K <= N`.
- Space: `O(1)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Longest%20Peak)