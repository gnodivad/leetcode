# 0160. Intersection of Two Linked Lists

## Approach 1: Brute Force
For each node in list A, traverse over list B and check whether or not the current node in list A is present in list B.

```Java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode currentA = headA;
        
        while (currentA != null) {
            ListNode currentB = headB;
            while (currentB != null) {
                if (currentA == currentB) return currentA;
                
                currentB = currentB.next;
            }
            
            currentA = currentA.next;
        }
        
        return null;
    }
}
```

### Time and Space Complexity

N = Length of List A, M = Length of List B
- Time: `O(N * M)`
- Space: `O(1)`

## References
- EPI 8.4