# 1091. Shortest Path in Binary Matrix

## Approach 1
First, we need to ensure the start cell and end cell is contains `0`. Then, we start to use BFS to expand the search from the start cell.

```Java
class Solution {
    public int shortestPathBinaryMatrix(int[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;
        
        if (grid[0][0] != 0 || grid[rows - 1][cols - 1] != 0) return -1;
        
        Deque<int[]> queue = new LinkedList<>();
        queue.addFirst(new int[]{0, 0});
        queue.addFirst(new int[]{-1, -1});
        
        int distance = 1;
        int[][] directions = new int[][]{ {-1, 0}, {-1, 1}, {0, 1}, {1, 1}, {1, 0}, {1, -1}, {0, -1}, {-1, -1}};
        
        while (!queue.isEmpty()) {
            int[] cell = queue.pollLast();
            int row = cell[0], col = cell[1];
            
            if (row == -1 && col == -1) {
                distance++;
                
                if (!queue.isEmpty()) {
                    queue.addFirst(new int[]{-1, -1});
                }
            } else if (row == rows - 1 && col == cols - 1) {
                return distance;
            } else {
                for (int[] direction : directions) {
                    int newRow = row + direction[0];
                    int newCol = col + direction[1];
                    
                    if (newRow < 0 || newRow >= rows) continue;
                    if (newCol < 0 || newCol >= cols) continue;
                    if (grid[newRow][newCol] == 1) continue;
                    
                    grid[newRow][newCol] = 1;
                    queue.addFirst(new int[]{newRow, newCol});
                }
            }
        }
        
        return -1;
    }
}
```

### Time and Space Complexity

N = The size of the grid
- Time: `O(N)`
- Space: `O(N)`

## References
- None