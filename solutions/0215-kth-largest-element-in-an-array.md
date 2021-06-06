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

## Approach 2: Quickselect
We random select an element from the array and partition the remaining entries into those greater than the pivot and those less than the pivot. If we find kth largest element in array with size N, the element will be in the index `N - K` of sorted array. If the pivot index after partition is greater than k, we should focus on the subarray before pivot index. Otherwise, we should discard elements less than the pivot.

```Java
class Solution {
    int[] nums;
    
    public int findKthLargest(int[] nums, int k) {
        this.nums = nums;
        
        return quickselect(0, nums.length - 1, nums.length - k);
    }
    
    public int quickselect(int left, int right, int kSmallest) {
        if (left == right) return this.nums[left];
        
        Random randomGenerator = new Random();
        int pivotIndex = left + randomGenerator.nextInt(right - left);
        pivotIndex = partition(left, right, pivotIndex);
        
        if (kSmallest == pivotIndex) {
            return this.nums[kSmallest];
        } else if (kSmallest < pivotIndex) {
            return quickselect(left, pivotIndex - 1, kSmallest);
        } else {
            return quickselect(pivotIndex + 1, right, kSmallest);
        }
    }
    
    public int partition(int left, int right, int pivotIndex) {
        int pivot = this.nums[pivotIndex];
        
        swap(pivotIndex, right);
        
        int smallerValueIndex = left;
        for (int i = left; i <= right; i++) {
            if (this.nums[i] < pivot) {
                swap(smallerValueIndex, i);
                smallerValueIndex++;
            }
        }
        
        swap(smallerValueIndex, right);
        
        return smallerValueIndex;
    }
    
    public void swap(int a, int b) {
        int tmp = this.nums[a];
        this.nums[a] = this.nums[b];
        this.nums[b] = tmp;
    }
}
```

### Time and Space Complexity

N = Length of the array `nums`, K = Value of `k`
- Time: `O(NLog(K))`
- Space: `O(Log(K))`

## References
- EPI 12.8