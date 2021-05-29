# 0684. Redundant Connection

## Approach 1: Union Find
Try to union all the edges and the union function will return error when both of the verticle is belongs to the same root.

```Java
class Solution {
    public int[] findRedundantConnection(int[][] edges) {
        UnionFind uf = new UnionFind(edges.length);
        
        int[] cycleEdge = new int[2];
        for (int[] edge : edges) {
            if (!uf.unify(edge[0] - 1, edge[1] - 1)) {
                cycleEdge = edge;
            }
        }
        
        return cycleEdge;
    }
}

class UnionFind {
    private int[] ids;
    private int[] sizes;
    private int numComponents;
    
    public UnionFind(int size) {
        numComponents = size;
        ids = new int[size];
        sizes = new int[size];
        
        for (int i = 0; i < size; i++) {
            ids[i] = i;
            sizes[i] = 1;
        }
    }
    
    public int find(int p) {
        int root = p;
        while (root != ids[root]) {
            root = ids[root];
        }
        
        while (p != root) {
            int next = ids[p];
            ids[p] = root;
            p = next;
        }
        
        return root;
    }
    
    public boolean unify(int p, int q) {
        int root1 = find(p);
        int root2 = find(q);
        
        if (root1 == root2) return false;
        
        if (sizes[root1] < sizes[root2]) {
            sizes[root2] += sizes[root1];
            ids[root1] = root2;
        } else {
            sizes[root1] += sizes[root2];
            ids[root2] = root1;
        }
        
        numComponents--;
        
        return true;
    }
}
```

### Time and Space Complexity

H = Number of vertices
- Time: `O(N)`
- Space: `O(N)`

## References
- None