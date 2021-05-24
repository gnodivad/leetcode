# 0841. Keys and Rooms

## Approach 1: DFS
Use DFS to nagivate the rooms. First, let add the first room to a stack and mark it as visited. After that, pushed all the room into stack which the current room have keys to open it and it never been visit before. Repeat this process until the stack is empty.

```Java
class Solution {
    public boolean canVisitAllRooms(List<List<Integer>> rooms) {
        boolean[] seen = new boolean[rooms.size()];
        seen[0] = true;
        
        Deque<Integer> stack = new LinkedList();
        stack.push(0);
        
        while(!stack.isEmpty()) {
            int node = stack.pop();
            
            for (int neighbour : rooms.get(node)) {
                if (!seen[neighbour]) {
                    seen[neighbour] = true;
                    stack.push(neighbour);
                }
            }
        }
        
        for (boolean v : seen) {
            if (v == false) return false;
        }
        
        return true;
    }
}
```

### Time and Space Complexity

N = Number of rooms, E = Total of keys
- Time: `O(N+E)`
- Space: `O(N)`

## References
- None