# 0622. Design Circular Queue

## Approach 1: Array

```java
class MyCircularQueue {
    int head = 0, size = 0;
    int[] queue;

    public MyCircularQueue(int k) {
        queue = new int[k];
    }
    
    public boolean enQueue(int value) {
        if (this.isFull()) return false;
        
        queue[(head + size) % queue.length] = value;
        
        size++;
        return true;
    }
    
    public boolean deQueue() {
        if (this.isEmpty()) return false;
        
        head = (head + 1) % queue.length;
        size--;
        return true;
    }
    
    public int Front() {
        if (this.isEmpty()) return -1;
        
        return queue[head];
    }
    
    public int Rear() {
        if (this.isEmpty()) return -1;
        
        return queue[(head + size - 1) % queue.length];
    }
    
    public boolean isEmpty() {
        return size == 0;
    }
    
    public boolean isFull() {
        return size == queue.length;
    }
}

/**
 * Your MyCircularQueue object will be instantiated and called as such:
 * MyCircularQueue obj = new MyCircularQueue(k);
 * boolean param_1 = obj.enQueue(value);
 * boolean param_2 = obj.deQueue();
 * int param_3 = obj.Front();
 * int param_4 = obj.Rear();
 * boolean param_5 = obj.isEmpty();
 * boolean param_6 = obj.isFull();
 */
```

### Time and Space Complexity

N = Length of the array
- Time: `O(1)`
- Space: `O(N)`

## References
- EPI 9.8