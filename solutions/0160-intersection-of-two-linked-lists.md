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

## Approach 2: Two Pointers
Calculate the size of two list as `N` and `M`. The "tails" must be same length, we can conclude that if there is an intersection, the intersection will be one of those node in the last `Math.min(N, M)`. We can advance the pointer in longer list by `Math.abs(N - M)`. After that, we can advance two pointer together to find the intersection node.

Side Note: Let assume `c` is the length of both linked list, `a` is the length of list A exclude the shared node, and `b` is the length of list B exclude the shared node. We can have one pointer goes over `a + c + b` and the other pointer goes over `b + c + a`. Since they are traverse in the same speed, they eventually will meet at the intersection node. When there is no intersection, both pointer will end up in the end of linked list at the same time.

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
        int sizeA = getLength(headA);
        int sizeB = getLength(headB);
        
        int advanceByK = Math.abs(sizeA - sizeB);
        
        ListNode longList, shortList;
        if (sizeA > sizeB) {
            longList = headA;
            shortList = headB;
        } else {
            longList = headB;
            shortList = headA;
        }
        
        while (advanceByK-- > 0) {
            longList = longList.next;
        }
        
        while (longList != null && shortList != null) {
            if (longList == shortList) return longList;
            
            longList = longList.next;
            shortList = shortList.next;
        }
        
        return null;
    }
    
    public int getLength(ListNode head) {
        ListNode current = head;
        
        int count = 0;
        while (current != null) {
            count++;
            current = current.next;
        }
        
        return count;
    }
}
```

### Time and Space Complexity

N = Length of List A, M = Length of List B
- Time: `O(N + M)`
- Space: `O(1)`

## References
- EPI 8.4