# 1020. Number of Enclaves

## Approach 1
First, let us add all the border cell into a list to acts as the starting point of DFS. After that, we can marked all the cell that connected to that border cell mark as `2` in-place. We will get three state of the cell after we iterate all the border cells (`0`, `1`, `2`). The total of `1` inside the grid is the cell that is not connected to the border cell.

```Java
class Solution {
    private int ROWS;
    private int COLS;
    
    public int numEnclaves(int[][] grid) {
        this.ROWS = grid.length;
        this.COLS = grid[0].length;
        
        List<Pair> points = new ArrayList<>();
        
        for (int r = 0; r < this.ROWS; r++) {
            points.add(new Pair(r, 0));
            points.add(new Pair(r, this.COLS - 1));
        }
        
        for (int c = 0; c < this.COLS; c++) {
            points.add(new Pair(0, c));
            points.add(new Pair(this.ROWS - 1, c));
        }
        
        for (Pair point : points) {
            dfs(grid, point.u, point.v);
        }
        
        int count = 0;
        for (int i = 0; i < this.ROWS; i++) {
            for (int j = 0; j < this.COLS; j++) {
                if (grid[i][j] == 1) count++;
            }
        }
        
        return count;
    }
    
    public void dfs(int[][] grid, int r, int c) {
        if (
            r < 0 ||
            r >= this.ROWS ||
            c < 0 ||
            c >= this.COLS
        ) {
            return;
        }
        
        if (grid[r][c] != 1) return;
        
        grid[r][c] = 2;
        dfs(grid, r, c + 1);
        dfs(grid, r + 1, c);
        dfs(grid, r, c - 1);
        dfs(grid, r - 1, c);
    }
}

class Pair {
    public int u;
    public int v;
    
    public Pair(int u, int v) {
        this.u = u;
        this.v = v;
    }
}
```

### Time and Space Complexity

N = the number of cells in `grid`
- Time: `O(N)`
- Space: `O(N)`

## References
- None