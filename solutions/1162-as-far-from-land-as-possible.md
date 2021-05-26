# 1162. As Far from Land as Possible

## Approach 1
Matrix cell contains `1`, which is land will acts as start node for BFS in the queue. When using BFS, the search will expanding outward from each land cell and ignore the cell that are visited by another land cell.

```Java
class Solution {    
    public int maxDistance(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        
        Deque<int[]> queue = new LinkedList<>();
        boolean[][] visited = new boolean[m][n];
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1) {
                    queue.add(new int[]{i, j});
                    visited[i][j] = true;
                }
            }
        }
        
        int distance = -1;
        while (!queue.isEmpty()) {
            int sameLevelCell = queue.size();
            distance++;
            
            for (int cell = 0; cell < sameLevelCell; cell++) {
                int[] currentCell = queue.pollLast();
                int row = currentCell[0];
                int col = currentCell[1];
                
                if (row > 0 && !visited[row - 1][col]) {
                    queue.addFirst(new int[]{row - 1, col});
                    visited[row - 1][col] = true;
                }
                if (col < n - 1 && !visited[row][col + 1]) {
                    queue.addFirst(new int[]{row, col + 1});
                    visited[row][col + 1] = true;
                }
                if (row < m - 1  && !visited[row + 1][col]) {
                    queue.addFirst(new int[]{row + 1, col});
                    visited[row + 1][col] = true;
                }
                if (col > 0  && !visited[row][col - 1]) {
                    queue.addFirst(new int[]{row, col - 1});
                    visited[row][col - 1] = true;
                }
            }            
        }
        
        return distance <= 0 ? -1 : distance;
    }
}
```

### Time and Space Complexity

r = the total of row `grid`, c = the total of column `grid`
- Time: `O(rc)`
- Space: `O(rc)`

## References
- None