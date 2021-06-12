# 0150. Evaluate Reverse Polish Notation

## Approach 1: Stack
Push the integer into stack. Pop two number out if current string contains any character of "+", "-", "*", and "/".

```Java
class Solution {
    public int evalRPN(String[] tokens) {
        Deque<Integer> stack = new LinkedList<>();
        
        for (String token : tokens) {
            if (!"+-*/".contains(token)) {
                stack.push(Integer.valueOf(token));
                continue;
            }
            
            int number2 = stack.pop();
            int number1 = stack.pop();
            
            int result = 0;
            switch (token) {
                case "+":
                    result = number1 + number2;
                    break;
                case "-":
                    result = number1 - number2;
                    break;
                case "*":
                    result = number1 * number2;
                    break;
                case "/":
                    result = number1 / number2;
                    break;
            }
            
            stack.push(result);
        }
        
        return stack.pop();
    }
}
```

### Time and Space Complexity

N = Length of tokens
- Time: `O(N)`
- Space: `O(N)`

## References
- None