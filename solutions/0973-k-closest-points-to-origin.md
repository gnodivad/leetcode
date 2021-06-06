# 0973. K Closest Points to Origin

## Approach 1: Heap
Compute the distance for each array element in the array `points` and add them to a maxHeap. When the size maxHeap is greater than `k`, discard the top element, which is the largest element in the heap.

```Java
class Solution {
    public int[][] kClosest(int[][] points, int k) {
        PriorityQueue<Point> minHeap = new PriorityQueue<Point>((a, b) -> -Double.compare(a.distance, b.distance));
        
        for (int[] point : points) {
            minHeap.add(new Point(point));
            
            if (minHeap.size() > k) {
                minHeap.remove();
            }
        }
        
        int[][] answers = new int[k][2];
        for (int i = 0; i < k; i++) {
            Point point = minHeap.poll();
            answers[i] = point.coordinate;
        }
        
        return answers;
    }
}

class Point {
    int[] coordinate;
    double distance;
    
    public Point(int[] coordinate) {
        this.coordinate = coordinate;
        this.distance = Math.sqrt((coordinate[0] * coordinate[0]) + (coordinate[1] * coordinate[1]));
    }
}
```

### Time and Space Complexity

N = Length of the array `points`, K = Value of `k`
- Time: `O(NLog(K))`
- Space: `O(K)`

## References
- EPI 11.4