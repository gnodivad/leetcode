# 0146. LRU Cache

## Approach 1: Recursive
Use LinkedHashMap to construct the cache. If turn on ordering, the default will be from the least-recently accessed to most-recently-accessed.

```Java
class LRUCache extends LinkedHashMap<Integer, Integer> {
    private int capacity;
    
    public LRUCache(int capacity) {
        super(capacity, 0.75F, true);
        this.capacity = capacity;
    }
    
    public int get(int key) {
        return super.getOrDefault(key, -1);
    }
    
    public void put(int key, int value) {
        super.put(key, value);
    }
    
    @Override
    protected boolean removeEldestEntry(Map.Entry<Integer, Integer> eldest) {
        return size() > capacity; 
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

### Time and Space Complexity

N = total number of node in the tree
- Time: `O(1)`
- Space: `O(capacity)`

## References
- None