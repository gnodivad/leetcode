# 0787. Cheapest Flights Within K Stops

## Approach 1: Dijkstra's Algorithm
A little tweak need to done to apply Dijkstra's Algorithm on this problem. Besides keep track on the distance, we also need to keep track on the total number of stops. Add the city to the `minHeap` if the shorter distance and lesser stop is found when reach a city.

```Java
class Solution {
    public int findCheapestPrice(int n, int[][] flights, int src, int dst, int k) {
        HashMap<Integer, ArrayList<int[]>> graph = new HashMap<>();
        for (int[] flight : flights) {
            if (!graph.containsKey(flight[0])) graph.put(flight[0], new ArrayList<>());
            if (!graph.containsKey(flight[1])) graph.put(flight[1], new ArrayList<>());
            graph.get(flight[0]).add(new int[]{flight[1], flight[2]});
        }
        
        int[] distances = new int[n];
        
        int[] currentStops = new int[n];
        Arrays.fill(distances, Integer.MAX_VALUE);
        Arrays.fill(currentStops, Integer.MAX_VALUE);
        distances[src] = 0;
        currentStops[src] = 0;
        
        PriorityQueue<int[]> minHeap = new PriorityQueue<int[]>((a , b) -> a[1] - b[1]);
        minHeap.offer(new int[]{src, 0, 0});
        
        while (!minHeap.isEmpty()) {
            int[] info = minHeap.poll();
            int node = info[0], cost = info[1], stops = info[2];
            
            if (node == dst) return cost;
            if (stops == k + 1) continue;
            
            if (!graph.containsKey(node)) continue;
            for (int[] neighbour : graph.get(node)) {
                int newCost = cost + neighbour[1];
                if (newCost < distances[neighbour[0]]) {
                    distances[neighbour[0]] = newCost;
                    currentStops[neighbour[0]] = stops;
                    minHeap.offer(new int[]{neighbour[0], newCost, stops + 1});
                } else if (stops < currentStops[neighbour[0]]) {
                    distances[neighbour[0]] = newCost;
                    currentStops[neighbour[0]] = stops;
                    minHeap.offer(new int[]{neighbour[0], newCost, stops + 1});
                }
            }
        }
        
        return distances[dst] == Integer.MAX_VALUE? -1 : distances[dst];
    }
}
```

### Time and Space Complexity

V = Number of city, E = Number of edge
- Time: `O(V.V.log(V))`
- Space: `O(VE)`

## References
- None