# 0994. Rotting Oranges

## Approach 1: BFS
Scan through the grid to find out the total of fresh oranges and put the rotten oranges into queue for BFS. We can skip processing if the total of fresh orange is `0` in the beginning. Inside the iteration, we will mark the neighbour of rotten oranges as rotten, decrease the total of fresh oranges, and put them into queue for processing later. In the end, all the connected oranges with rotten oranges will be processed.

```Java
class Solution {
    public int orangesRotting(int[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;
        
        Deque<int[]> queue = new LinkedList<>();
        
        int freshOranges = 0;
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (grid[i][j] == 2) {
                    queue.addFirst(new int[]{i, j});
                } else if (grid[i][j] == 1) {
                    freshOranges++;
                }
            }
        }
        
        if (freshOranges == 0) return 0;
        
        int time = -1;
        while (!queue.isEmpty()) {
            int size = queue.size();
            time++;
            
            for (int i = 0; i < size; i++) {
                int[] cell = queue.pollLast();
                int row = cell[0];
                int col = cell[1];
                                
                if (row > 0 && grid[row - 1][col] == 1) {
                    queue.addFirst(new int[]{row - 1, col});
                    grid[row - 1][col] = 2;
                    freshOranges--;
                }
                
                if (col < cols - 1 && grid[row][col + 1] == 1) {
                    queue.addFirst(new int[]{row, col + 1});
                    grid[row][col + 1] = 2;
                    freshOranges--;
                }
                
                if (row < rows - 1 && grid[row + 1][col] == 1) {
                    queue.addFirst(new int[]{row + 1, col});
                    grid[row + 1][col] = 2;
                    freshOranges--;
                }
                
                if (col > 0 && grid[row][col - 1] == 1) {
                    queue.addFirst(new int[]{row, col - 1});
                    grid[row][col - 1] = 2;
                    freshOranges--;
                }
            }
        }
        
        return freshOranges == 0 ? time : -1;
    }
}
```

### Time and Space Complexity

N = the size of the grid
- Time: `O(N)`
- Space: `O(N)`

## References
- None