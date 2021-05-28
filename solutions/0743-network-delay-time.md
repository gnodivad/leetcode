# 0743. Network Delay Time

## Approach 1: Dijkstra's Algorithm
Construct the graph with HashMap that each of the entry is the combination of int and another HashMap. The another HashMap use to store all the neighbour and the cost to traverse there. Apply Dijkstra's Algorithm on the start node `k` and update all its neighbours cost. Find the node that have smallest cost to continue to the next iteration provided that node never visited before.

```Java
class Solution {
    HashSet<Integer> visited;
    int[] distances;
    
    public int networkDelayTime(int[][] times, int n, int k) {
        HashMap<Integer, HashMap<Integer, Integer>> graph = new HashMap<>();
        this.visited = new HashSet<>();
        for (int i = 1; i <= n; i++) {
            graph.put(i, new HashMap<Integer, Integer>());
        }
        
        for (int[] time : times) {
            graph.get(time[0]).put(time[1], time[2]);
        }
        
        this.distances = new int[n + 1];
        Arrays.fill(this.distances, Integer.MAX_VALUE);
        
        this.distances[k] = 0;
        Integer node = k;
        while (node != null) {
            int cost = this.distances[node];
            
            for (Map.Entry<Integer, Integer> neighbour: graph.get(node).entrySet()) {
                int newCost = cost + neighbour.getValue();
                this.distances[neighbour.getKey()] = Math.min(
                    this.distances[neighbour.getKey()], 
                    newCost
                );
            }
            this.visited.add(node);
            
            node = findNextNode();
        }
        
        int maxDistance = 0;
        for (int i = 1; i < this.distances.length; i++) {
            maxDistance = Math.max(maxDistance, this.distances[i]);
        }
        
        return maxDistance == Integer.MAX_VALUE ? -1 : maxDistance;
    }
    
    public Integer findNextNode() {
        Integer node = null;
        Integer minCost = Integer.MAX_VALUE;
        
        for (int i = 1; i < this.distances.length; i++) {
            if (this.distances[i] < minCost && !this.visited.contains(i)) {
                node = i;
                minCost = this.distances[i];
            }
        }

        return node;
    }
}
```

### Time and Space Complexity

V = Total of verticle, E = Total of edge
- Time: `O(VE)`
- Space: `O(V + E)`

## References
- None