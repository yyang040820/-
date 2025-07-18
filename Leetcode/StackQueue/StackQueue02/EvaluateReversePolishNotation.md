## 150. Evaluate Reverse Polish Notation

题目链接:[Evaluate Reverse Polish Notation]

题意： 
You are given an array of strings tokens that represents an arithmetic expression in a Reverse Polish Notation.

Evaluate the expression. Return an integer that represents the value of the expression.

Note that:

The valid operators are '+', '-', '*', and '/'.
Each operand may be an integer or another expression.
The division between two integers always truncates toward zero.
There will not be any division by zero.
The input represents a valid arithmetic expression in a reverse polish notation.
The answer and all the intermediate calculations can be represented in a 32-bit integer.
 

Example 1:

Input: tokens = ["2","1","+","3","*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9
Example 2:

Input: tokens = ["4","13","5","/","+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
Example 3:

Input: tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
Output: 22
Explanation: ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22


#### 简洁回答
用栈按后缀表达式（逆波兰表示法）计算：遍历 `tokens`，遇到数字就压栈，遇到运算符就弹出两个栈顶元素计算并将结果入栈；遍历结束后栈顶即为答案。注意 Python 中除法需向零取整，可用 `int(a/b)` 实现。时间复杂度 O(N)，空间复杂度 O(N)。

#### 详细回答
1. **数据结构**  
   使用一个栈 `stack` 来保存中间结果。

2. **遍历输入**  
   - 如果当前 `token` 不是运算符，就将 `int(token)` 入栈。  
   - 如果是运算符，就依次弹出 `first = stack.pop()`（右操作数）和 `second = stack.pop()`（左操作数），根据运算符执行对应计算：
     - `+`：`second + first`  
     - `-`：`second - first`  
     - `*`：`second * first`  
     - `/`：`int(second / first)` ——保证结果向零取整，符合题意（如 `-3/2 = -1`）。

3. **结果输出**  
   最终 `stack` 中只剩一个元素，即为表达式的计算结果，直接返回即可。

```python
def evalRPN(self, tokens: List[str]) -> int:
        stack = []
        operations = ['+','-','*','/']
        ans = 0

        for token in tokens:
            if token not in operations:
                stack.append(int(token))
                continue
            first_num = stack.pop()
            second_num = stack.pop()
            if token == '/':
                ans = int(second_num / first_num)
            elif token == '+':
                ans = second_num + first_num
            elif token == '*':
                ans = second_num * first_num
            else:
                ans = second_num - first_num
            stack.append(int(ans))
        
        return stack[-1]
```
