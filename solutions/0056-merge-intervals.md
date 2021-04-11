# 0056. Merge Intervals

## Approach 1: Sorting
Sort the intervals by their `start` value, after that we just need to focus on `end` value. First, we use the first interval to determine that the next interval `start` is less than or equal to. If yes, we just need to alter the first interval `end` to the maximum `end` value between first interval and next interval. Otherwise, we can just append the interval to the `mergedInterval` since it does not intersect with next interval.

```Java
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        
        List<int[]> mergedInterval = new ArrayList<>();
        int[] currentInterval = intervals[0];
        
        for (int i = 1; i < intervals.length; i++) {
            if (intervals[i][0] > currentInterval[1]) {
                mergedInterval.add(currentInterval);
                currentInterval = intervals[i];
            } else {
                currentInterval[1] = Math.max(currentInterval[1], intervals[i][1]);
            }
        }
        
        mergedInterval.add(currentInterval);
        
        return mergedInterval.toArray(new int[mergedInterval.size()][]);
    }
}
```

### Time and Space Complexity

N = total number of elements in the input `intervals`
- Time: `O(NLog(N))`
- Space: `O(N)`

## Approach 2: Connected Components
Build a graph with intervals as node and they linked each other with undirected edges if there is an overlap. After that, travel the graph with DFS and group each of the node into connected components. Then, merge all intervals in each connected compoinent into single interval.

```Java
class Solution {
    private Map<int[], List<int[]>> graph;
    private Map<Integer, List<int[]>> nodesInComp;
    private Set<int[]> visited;
    
    private boolean overlap(int[] a, int[] b) {
        return a[0] <= b[1] && b[0] <= a[1];
    }
    
    private void buildGraph(int[][] intervals) {
        graph = new HashMap<>();
        
        for (int[] interval: intervals) {
            graph.put(interval, new LinkedList<>());
        }
        
        for (int i = 0; i < intervals.length; i++) {
            for (int j = i + 1; j < intervals.length; j++) {
                if (overlap(intervals[i], intervals[j])) {
                    graph.get(intervals[i]).add(intervals[j]);
                    graph.get(intervals[j]).add(intervals[i]);
                }
            }
        }
    }
    
    private void markComponentDFS(int[] start, int compNumber) {
        Stack<int[]> stack = new Stack<>();
        stack.add(start);
        
        while (!stack.isEmpty()) {
            int[] node = stack.pop();
            if (!visited.contains(node)) {
                visited.add(node);
                
                if (nodesInComp.get(compNumber) == null) {
                    nodesInComp.put(compNumber, new LinkedList<>());
                }

                nodesInComp.get(compNumber).add(node);

                for (int[] child : graph.get(node)) {
                    stack.add(child);
                }
            }
        }
    }
    
    private void buildComponents(int[][] intervals) {
        nodesInComp = new HashMap<>();
        visited = new HashSet<>();
        int compNumber = 0;
        
        for (int[] interval : intervals) {
            if (!visited.contains(interval)) {
                markComponentDFS(interval, compNumber);
                compNumber++;
            }
        }
    }
    
    private int[] mergeNodes(List<int[]> nodes) {
        int minStart = nodes.get(0)[0], maxEnd = nodes.get(0)[1];
        for (int[] node : nodes) {
            minStart = Math.min(minStart, node[0]);
            maxEnd = Math.max(maxEnd, node[1]);
        }

        return new int[] {minStart, maxEnd};
    }
    
    public int[][] merge(int[][] intervals) {
        buildGraph(intervals);
        buildComponents(intervals);
        
        List<int[]> merged = new LinkedList<>();
        for (int comp = 0; comp < nodesInComp.size(); comp++) {
            merged.add(mergeNodes(nodesInComp.get(comp)));
        }
        
        return merged.toArray(new int[merged.size()][]);
    }
}
```

### Time and Space Complexity

N = total number of elements in the input `intervals`, V = vertex of the graph, E = edges of the graph
- Time: `O(N^2)`
    - Building the graph costs `O(V+E)` = `O(V) + O(E)` = `O(N) + O(N^2)` = `O(N^2)`
    - Traverse the graph costs  `O(N^2)`. Although we keep visited node in `visited`, but it still need to traverse the edge before it will lead to the vertex already visted before.
    - Merge the connected components costs `O(N)` since each of the node have exactlty one connected components.
- Space: `O(N^2)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Merge%20Overlapping%20Intervals)