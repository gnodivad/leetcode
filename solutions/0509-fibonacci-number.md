# 0509. Fibonacci Number

## Approach 1: Recursion
Use recursion to compute fibonacci that is larger than `1`. Two base case for this recursion is `fib(0) = 0` and `fib(1) = 1`.

```java
class Solution {
    public int fib(int n) {
        if (n == 0) return 0;
        if (n == 1) return 1;
        
        return fib(n - 1) + fib(n - 2);
    }
}
```

### Time and Space Complexity
N = Nth of fibonacci number
- Time: `O(2^N)`
- Space: `O(N)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Nth%20Fibonacci)