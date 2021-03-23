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

## Approach 2: Recursion with Memoization
Approach 1 will keep repeating compute value for subproblem, for example the function to compute for `f(4)` will compute `f(2)` two times. It is unefficient when we are find fibonacci number that in bigger nth. We can use memoization to store the pre-computed answers. The result of `f(2)` will store in HashMap for example above and the second times for `f(2)` will retrieve from HashMap instead of compute again.

```java
class Solution {
    public int fib(int n) {
        HashMap<Integer, Integer> memo = new HashMap<>();
        memo.put(0, 0);
        memo.put(1, 1);
        
        return fib(n, memo);
    }
    
    public int fib(int n, HashMap<Integer, Integer> memo) {
        if (memo.containsKey(n)) {
            return memo.get(n);
        }
        
        int result = fib(n - 1) + fib(n - 2);
        memo.put(n, result);
        
        return result;
    }
}
```

### Time and Space Complexity
N = Nth of fibonacci number
- Time: `O(N)`
- Space: `O(N)`

## Approach : Recursion
The computation of nth fibonacci only care about `n-1`th fibonacci number and `n-2`th fibonacci number. We just need store both of them in an array that have length 2 and updating them as we iterate to `n`.

```java
class Solution {
    public int fib(int n) {
        int[] memo = {0, 1};
        
        int counter = 2;
        while (counter <= n) {
            int result = memo[0] + memo[1];
            memo[0] = memo[1];
            memo[1] = result;
            counter++;
        }
        
        return n > 0 ? memo[1] : memo[0];
    }
}
```

### Time and Space Complexity
N = Nth of fibonacci number
- Time: `O(N)`
- Space: `O(1)`

## References
- [AlgoExpert](https://www.algoexpert.io/questions/Nth%20Fibonacci)