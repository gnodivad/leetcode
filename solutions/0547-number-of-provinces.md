# 0547. Number of Provinces

## Approach 1
Use Union Find operation on all the connected city.

```java
class Solution {
    public int findCircleNum(int[][] isConnected) {
        UnionFind uf = new UnionFind(isConnected.length);
        
        for (int i = 0; i < isConnected.length; i++) {
            for (int j = 0; j < isConnected[i].length; j++) {
                if (i == j) continue;
                
                if (isConnected[i][j] == 1) {
                    uf.unify(i, j);
                }
            }
        }
        
        return uf.components();
    }
}

class UnionFind {
    private int[] sizes;
    private int[] components;
    private int numComponents;
    
    public UnionFind(int size) {
        numComponents = size;
        sizes = new int[size];
        components = new int[size];
        
        for (int i = 0; i < size; i++) {
            components[i] = i;
            sizes[i] = 1;
        }
    }
    
    public int find(int p) {
        int root = p;
        while (root != components[root]) {
            root = components[root];
        }
        
        while (p != root) {
            int next = components[p];
            components[p] = root;
            p = next;
        }
        
        return root;
    }
    
    public int components() {
        return numComponents;
    }
    
    public void unify(int p, int q) {
        int root1 = find(p);
        int root2 = find(q);
        
        if (root1 == root2) return;
        
        if (sizes[root1] < sizes[root2]) {
            sizes[root2] += sizes[root1];
            components[root1] = root2;
        } else {
            sizes[root1] += sizes[root2];
            components[root2] = root1;
        }
        
        numComponents--;
    }
}
```

### Time and Space Complexity
N = total of node in binary tree
- Time: `O(N^3)`
    - `O(N ^ 2)` traverse the matrix
    - `O(N)` for UnionFind Operation
- Space: `O(N)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Binary%20Tree%20Diameter)