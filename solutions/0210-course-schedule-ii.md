# 0210. Course Schedule II

## Approach 1: Topological Sort
Construct the graph from `prerequisites` array by using a `GNode` class and HashMap. Every course's label will become a key in HashMap and GNode as value. GNode will contain all the information about the total number of node that directed edges to this node `inDegrees` and an array of all the node that it points to `outNodes`. During the start, we scan through all the node to add all those without dependency into a stack. Each time, we will iterate through all their neighbour node to the stack and decrease the `inDegrees`. If the `inDegrees` reach 0, then we will add it to the stack. Repeat this process until the stack is empty.

```Java
class GNode {
    public Integer inDegrees = 0;
    public List<Integer> outNodes = new LinkedList<Integer>();
}

class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        if (prerequisites.length == 0) return IntStream.range(0, numCourses).toArray();
        
        int[] ordering = new int[numCourses];
        int orderingIdx = 0;
        
        HashMap<Integer, GNode> graph = new HashMap<>();        
        for (int[] relationship : prerequisites) {
            GNode prevCourse = this.getCreateGNode(graph, relationship[1]);
            GNode nextCourse = this.getCreateGNode(graph, relationship[0]);
            prevCourse.outNodes.add(relationship[0]);
            nextCourse.inDegrees++;    
        }
        
        Deque<Integer> stack = new LinkedList<>();
        for (int i = 0; i < numCourses; i++) {
            if (!graph.containsKey(i)) {
                ordering[orderingIdx++] = i;
            } else if (graph.get(i).inDegrees == 0) {
                stack.push(i);
                ordering[orderingIdx++] = i;
            }
        }
        
        int totalDependency = prerequisites.length;
        while (!stack.isEmpty()) {
            int currentNode = stack.pop();
            
            for (int neighbour : graph.get(currentNode).outNodes) {
                GNode nextNode = graph.get(neighbour);
                nextNode.inDegrees--;
                totalDependency--;
                
                if (nextNode.inDegrees == 0) {
                    stack.push(neighbour);
                    ordering[orderingIdx++] = neighbour;
                }
            }
        }
        
        return totalDependency == 0 ? ordering : new int[]{};
    }
    
    protected GNode getCreateGNode(HashMap<Integer, GNode> graph, Integer course) {
        GNode node = null;
        if (graph.containsKey(course)) {
            node = graph.get(course);
        } else {
            node = new GNode();
            graph.put(course, node);
        }
        
        return node;
    }
}
```

### Time and Space Complexity

V = number of courses, V = number of dependency
- Time: `O(E+V)`
- Space: `O(E+V)`

## References
- None