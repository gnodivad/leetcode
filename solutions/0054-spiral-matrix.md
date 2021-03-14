# 0054. Spiral Matrix

## Approach 1
Use four variable to keep track the boundaries of each iteration. Each iteration will consist four loops that scan from top left to top right, from top right to bottom right, from bottom right to bottom left and from bottom left back to top right. There are two things we need to pay attention at, which are:
- Avoid to target the element twice that are placed on the intersection of each loops
- Avoid repeat the same row from left to right and right to left again when the array has only one row, and repeat the same column from top to bottom, and bottom to top when the array has only one column.

```Java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        int startRow = 0, startCol = 0;
        int endRow = matrix.length - 1, endCol = matrix[0].length - 1;
        
        List<Integer> results = new ArrayList<>();
        
        while (startRow <= endRow && startCol <= endCol) {
            for (int col = startCol; col <= endCol; col++) {
                results.add(matrix[startRow][col]);
            }
            
            for (int row = startRow + 1; row <= endRow; row++) {
                results.add(matrix[row][endCol]);
            }
            
            for (int col = endCol - 1; col >= startCol; col--) {
                if (endRow == startRow) break;
                results.add(matrix[endRow][col]);
            }
            
            for (int row = endRow - 1; row > startRow; row--) {
                if (startCol == endCol) break;
                results.add(matrix[row][startCol]);
            }
            
            startRow++;
            startCol++;
            endRow--;
            endCol--;
        }
        
        return results;
    }
}
```

### Time and Space Complexity

N = total number of elements in the input `matrix`
- Time: `O(N)`
- Space: `O(1)`
	- O(1) without considering the output array.
	- O(N) if the output array is taken into account.

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Spiral%20Traverse)