# 0346. Moving Average from Data Stream

## Approach 1: Double-ended Queue
Use the queue to store all the incoming `val` and sum it at the same time. Once the queue size is greater than the window limit that specify, remove the value at the front of the queue and substract it from the `sum`.

```Java
class MovingAverage {
    int totalSize = 0, sum = 0;
    Deque queue;
    
    /** Initialize your data structure here. */
    public MovingAverage(int size) {
        this.queue = new LinkedList<Integer>();
        this.totalSize = size;
    }
    
    public double next(int val) {
        if (queue.size() == totalSize) {
            sum -= (int)queue.pollFirst();
        }
        
        sum += val;
        queue.addLast(val);
        return (double) sum / queue.size();
    }
}

/**
 * Your MovingAverage object will be instantiated and called as such:
 * MovingAverage obj = new MovingAverage(size);
 * double param_1 = obj.next(val);
 */
```

### Time and Space Complexity

N = size of the window `size`
- Time: `O(1)`
- Space: `O(N)`
