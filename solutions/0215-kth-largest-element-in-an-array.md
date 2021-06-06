# 0215. Kth Largest Element in an Array

## Approach 1: Heap
Add the array element in `nums` into heap and maintain the size of heap to `k` so that the first item of heap item will be the kth largest value we want to find.

```Java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> heap = new PriorityQueue<>((a, b) -> a - b);
        
        for (int num : nums) {
            heap.add(num);
            
            if (heap.size() > k) {
                heap.poll();
            }
        }
        
        return heap.poll();
    }
}
```

### Time and Space Complexity

N = Length of the array `nums`, K = Value of `k`
- Time: `O(NLog(K))`
- Space: `O(Log(K))`

## References
- EPI 12.8