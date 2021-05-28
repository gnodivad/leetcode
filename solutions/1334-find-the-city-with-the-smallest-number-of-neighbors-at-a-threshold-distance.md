# 1334. Find the City With the Smallest Number of Neighbors at a Threshold Distance

## Approach 1: Dijkstra's Algorithm
Apply Dijkstra's Algorithm on every city. The requirement of the problem is return the city with larger number when the total of visited city is the same, so we start with the city with larger number first. Everytime we get the total of visited city that within the `distanceThereshold`, keep track with the total of visited city across all the city `totalOfVisitedCity` and mark it as possible city if the total of visited city is less than the global minimumOfTotalofVisitedCity.

```Java
class Solution {
    public int findTheCity(int n, int[][] edges, int distanceThreshold) {
        int city = 0;
        int totalOfVisitedCity = Integer.MAX_VALUE;
        
        Map<Integer, ArrayList<int[]>> graph = new HashMap<>();
        for (int[] edge : edges) {
            if (!graph.containsKey(edge[0])) graph.put(edge[0], new ArrayList<>());
            if (!graph.containsKey(edge[1])) graph.put(edge[1], new ArrayList<>());
            graph.get(edge[0]).add(new int[] {edge[1], edge[2]});
            graph.get(edge[1]).add(new int[] {edge[0], edge[2]});
        }
        
        for (int i = n - 1; i >= 0; i--) {
            int[] distances = new int[n];
            Arrays.fill(distances,Integer.MAX_VALUE);
            
            PriorityQueue<int[]> heap = new PriorityQueue<>((a, b) -> a[1] - b[1]);
            distances[i] = 0;
            heap.add(new int[]{i, 0});
            
            while (!heap.isEmpty()) {
                int[] heapItem = heap.poll();
                int currentCity = heapItem[0];
                int cost = heapItem[1];
                
                if (!graph.containsKey(currentCity)) continue;
                
                for (int[] neighbour : graph.get(currentCity)) {
                    int newCost = neighbour[1] + cost;
                    if (newCost < distances[neighbour[0]]) {
                        distances[neighbour[0]] = newCost;
                        heap.add(new int[]{neighbour[0], newCost});
                    }
                }
            }
            
            int count = 0;
            for (int distance : distances) {
                if (distance <= distanceThreshold) count++;
            }
            
            if (count < totalOfVisitedCity) {
                totalOfVisitedCity = count;
                city = i;
            }
        }
        
        return city;
    }
}
```

### Time and Space Complexity

V = total of the city, E = total of the path
- Time: `O(VE)`
- Space: `O(V + E)`

## References
- None