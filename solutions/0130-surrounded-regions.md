# 0130. Surrounded Regions

## Approach 1: DFS
First, let us add all the border cell into a list to acts as the starting point of DFS. After that, we can marked all the cell that connected to that border cell mark as 'E' in-place. We will get three state of the cell after we iterate all the border cells (`E`, `O`, `X`). We can restore `E` back to `O` and flip `O` to `X`

```Java
class Solution {
    protected Integer ROWS = 0;
    protected Integer COLS = 0;
    
    public void solve(char[][] board) {
        if (board == null || board.length == 0) return;
        
        this.ROWS = board.length;
        this.COLS = board[0].length;
        
        List<Pair<Integer, Integer>> borders = new LinkedList<Pair<Integer, Integer>>();
        
        for (int r = 0; r < this.ROWS; ++r) {
            borders.add(new Pair(r, 0));
            borders.add(new Pair(r, this.COLS - 1));
        }
        
        for (int c = 0; c < this.COLS; ++c) {
            borders.add(new Pair(0, c));
            borders.add(new Pair(this.ROWS - 1, c));
        }
        
        for (Pair<Integer, Integer> pair: borders) {
            this.dfs(board, pair.first, pair.second);
        }
        
        for (int r = 0; r < this.ROWS; r++) {
            for (int c = 0; c < this.COLS; c++) {
                if (board[r][c] == 'O') board[r][c] = 'X';
                if (board[r][c] == 'E') board[r][c] = 'O';
            }
        }
    }
    
    protected void dfs(char[][] board, int row, int col) {
        if (
            row < 0 ||
            row >= this.ROWS ||
            col < 0 ||
            col >= this.COLS
        ) {
            return;
        }
        
        if (board[row][col] != 'O') return;
        
        board[row][col] = 'E';
        this.dfs(board, row, col + 1);
        this.dfs(board, row + 1, col);
        this.dfs(board, row, col - 1);
        this.dfs(board, row - 1, col);
    }
}

class Pair<U, V> {
    public U first;
    public V second;

    public Pair(U first, V second) {
        this.first = first;
        this.second = second;
    }
}
```

### Time and Space Complexity

N = number of cells in the board
- Time: `O(N)`
- Space: `O(N)`

## References
- None