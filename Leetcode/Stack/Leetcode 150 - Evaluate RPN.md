- **Problem Link**: https://leetcode.com/problems/evaluate-reverse-polish-notation/?envType=study-plan-v2&envId=top-interview-150


## My Solution
```python
class Solution:
    def evalRPN(self, tokens):
        stack = []
        for token in tokens:
            if token.strip("-").isdigit():
                stack.append(int(token))
            else:
                b = stack.pop()
                a = stack.pop()
                if token == "+":
                    stack.append(a + b)
                elif token == "-":
                    stack.append(a - b)
                elif token == "*":
                    stack.append(a * b)
                else:
                    stack.append(int(float(a) / b))

        return stack.pop()
```

## Approach
- RPN works by definition very well with stacks
- Every time we encounter an operand, we pop the two last numbers and perform the operation. Then we add the result to the stack 
- If we don't encounter an operation, we add the number to the stack

**Category**: Stack


## Time and Space Complexity
- Time: $O(n)$
- Space:  $O(n)$
## Similar Problems
- [[Leetcode/Leetcode]]