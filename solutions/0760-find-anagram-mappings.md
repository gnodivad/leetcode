# 0760. Find Anagram Mappings

## Approach 1: Hash Table
Create HashTable to record the index of each elements in `B` and populate output array with the index that found in HashTable by using element in `A`.

```Java
class Solution {
    public int[] anagramMappings(int[] A, int[] B) {
        HashMap<Integer, Integer> map = new HashMap<>();
        
        for (int i = 0; i < B.length; i++) {            
            map.put(B[i], i);
        }
                
        int[] mappings = new int[A.length];
        for (int i = 0; i < A.length; i++) {
            mappings[i] = map.get(A[i]);
        }
        
        return mappings;
    }
}
```

### Time and Space Complexity

N = length of A
- Time: `O(N)`
- Space: `O(N)`

## References
- None