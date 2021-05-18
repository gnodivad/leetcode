# 0200. Number of Islands

## Approach 1: DFS
If the cells of a grid contains `1`, then it is a root node that trigger Depth First Search. During DFS, each of the node will marked itself as `0` and continue trigger DFS on its neighbour. The answer will be the same as the total of times DFS is triggered.

```Java
class Solution {
    public int numIslands(char[][] grid) {
        int size = 0;
        
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == '0') continue;
                
                size++;
                markIslandAsVisited(grid, i, j);
            }
        }
        
        return size;
    }
    
    public void markIslandAsVisited(char[][] grid, int i, int j) {
        if (
            i < 0 ||
            i >= grid.length ||
            j < 0 ||
            j >= grid[0].length ||
            grid[i][j] == '0'
        ) {
            return;
        }
        
        grid[i][j] = '0';
        markIslandAsVisited(grid, i - 1, j);
        markIslandAsVisited(grid, i + 1, j);
        markIslandAsVisited(grid, i, j - 1);
        markIslandAsVisited(grid, i, j + 1);
        
        return;
    }
}
```

### Time and Space Complexity

M = number of rows of array `grid`, N = number of columns of array `grid`
- Time: `O(MN)`
- Space: `O(MN)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/River%20Sizes)