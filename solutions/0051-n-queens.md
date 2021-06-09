# 0051. N-Queens

## Approach 1: Backtracking
Start with empty board and start to place the queen into every column for each row. Initialize three HashSet to track for the column index, diagonal index and anti-diagonal index. 
The challenge part is on how to track diagonal and anti-diagonal? Althought it is trickier, but there is chess board property we can make use of:
- every square on the same diagonal will have same value when `(row - col)`.
- every square on the same anti-diagonal will have same value when `(row + col)`.
Every time we try to placed an queen, we should calculate the diagonal and the anti-diagonal value it belongs to in addition to column. We keep track them to avoid put any queens in the same column, diagonal or anti-diagonal in the future computation.

```Java
class Solution {
    private int size;
    private List<List<String>> solutions = new ArrayList<List<String>>();
    
    public List<List<String>> solveNQueens(int n) {
        this.size = n;
        
        char[][] state = new char[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                state[i][j] = '.';
            }
        }
        
        solveNQueens(0, new HashSet<>(), new HashSet<>(), new HashSet<>(), state);
        
        return solutions;
    }
    
    public List<String> createBoard(char[][] state) {
        List<String> solution = new ArrayList<>();
        for (char[] stateRow : state) {
            solution.add(String.valueOf(stateRow));
        }
        
        return solution;
    }
    
    public void solveNQueens(int row, HashSet<Integer> cols, HashSet<Integer> diagonals, HashSet<Integer> antiDiagonals, char[][] state) {
        if (row == size) {
            solutions.add(createBoard(state));
            return;
        }
        
        for (int col = 0; col < size; col++) {
            int diagonal = row - col, antiDiagonal = row + col;
            
            if (cols.contains(col) || diagonals.contains(diagonal) || antiDiagonals.contains(antiDiagonal)) continue;
            
            cols.add(col);
            diagonals.add(diagonal);
            antiDiagonals.add(antiDiagonal);
            state[row][col] = 'Q';
            
            solveNQueens(row + 1, cols, diagonals, antiDiagonals, state);
            
            cols.remove(col);
            diagonals.remove(diagonal);
            antiDiagonals.remove(antiDiagonal);
            state[row][col] = '.';
        }
    }
}
```

### Time and Space Complexity

N = Number of queens = Size of the board
- Time: `O(N!)`
- Space: `O(N^2)`

## References
- EPI 16.2