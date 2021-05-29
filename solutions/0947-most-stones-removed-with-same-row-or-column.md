# 0947. Most Stones Removed with Same Row or Column

## Approach 1: Union Find
Apply the Union Find operation on each stone. If the stone have same row or same column, union them. In the end, the stones need to removed will be same as the difference between the total of stones and the total of components in the union find.

```Java
class Solution {
    public int removeStones(int[][] stones) {
        UnionFind uf = new UnionFind(stones.length);
        
        for (int i = 0; i < stones.length; i++) {
            for (int j = i + 1; j < stones.length; j++) {
                if (stones[i][0] == stones[j][0] || stones[i][1] == stones[j][1]) {
                    uf.unify(i, j);
                }
            }
        }
        
        return stones.length - uf.totalOfComponents();
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
    
    public int totalOfComponents() {
        return numComponents;
    }
    
    public void unify(int p, int q) {
        int root1 = find(p);
        int root2 = find(q);
        
        if (root1 == root2) return;
        
        if (sizes[root1] < sizes[root2]) {
            sizes[root2] += sizes[root1];
            ids[root1] = root2;
        } else {
            sizes[root1] += sizes[root2];
            ids[root2] = root1;
        }
        
        numComponents--;
    }
}
```

### Time and Space Complexity

N = number of stones
- Time: `O(N)`
- Space: `O(N)`

## References
- None