# 0207. Course Schedule

## Approach 1: Topological Sort
Construct the graph from `prerequisites` array by using a `GNode` class and HashMap. Every course's label will become a key in HashMap and GNode as value. GNode will contain all the information about the total number of node that directed edges to this node `inDegrees` and an array of all the node that it points to `outNodes`. During the start, we scan through all the node to add all those without dependency into a stack. Each time, we will iterate through all their neighbour node to the stack and decrease the `inDegrees`. If the `inDegrees` reach 0, then we will add it to the stack. Repeat this process until the stack is empty.

```Java
class GNode {
    public Integer inDegrees = 0;
    public List<Integer> outNodes = new LinkedList<Integer>();
}

class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        if (prerequisites.length == 0) return true;
        
        HashMap<Integer, GNode> graph = new HashMap<>();
        
        for (int[] relation: prerequisites) {
            GNode prevCourse = this.getCreateGNode(graph, relation[1]);
            GNode nextCourse = this.getCreateGNode(graph, relation[0]);
            prevCourse.outNodes.add(relation[0]);
            nextCourse.inDegrees += 1;
        }
        
        int totalDeps = prerequisites.length;
        Deque<Integer> stack = new LinkedList<Integer>();
        for (Map.Entry<Integer, GNode> entry: graph.entrySet()) {
            GNode node = entry.getValue();
            if (node.inDegrees == 0) {
                stack.push(entry.getKey());
            }
        }
        
        int removedEdges = 0;
        while (!stack.isEmpty()) {
            Integer course = stack.pop();
            
            for (Integer nextCourse : graph.get(course).outNodes) {
                GNode childNode = graph.get(nextCourse);
                childNode.inDegrees -= 1;
                removedEdges += 1;
                if (childNode.inDegrees == 0) {
                    stack.push(nextCourse);
                }
            }
        }
        
        return removedEdges != totalDeps ? false : true;
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