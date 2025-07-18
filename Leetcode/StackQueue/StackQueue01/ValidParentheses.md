## 20. Valid Parentheses

题目链接:[https://leetcode.com/problems/valid-parentheses/description/]

题意： 
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Every close bracket has a corresponding open bracket of the same type.
 

Example 1:

Input: s = "()"

Output: true

Example 2:

Input: s = "()[]{}"

Output: true

Example 3:

Input: s = "(]"

Output: false

Example 4:

Input: s = "([])"

Output: true

Example 5:

Input: s = "([)]"

Output: false

 

Constraints:

1 <= s.length <= 104
s consists of parentheses only '()[]{}'.

#### 简洁回答
利用栈结构可以高效判断括号字符串是否有效。遇到左括号时入栈，遇到右括号时检查是否与栈顶匹配，匹配则弹出，不匹配则为无效。最终栈为空表示字符串有效。

#### 详细回答
一个有效的括号字符串，在遍历过程中应该满足这样的规则：

- 当遇到左括号（如 `(`、`[`、`{`）时，将其压入栈中；
- 当遇到右括号（如 `)`、`]`、`}`）时，应该与栈顶的左括号配对；
  - 如果栈不为空且栈顶元素与当前右括号匹配，则将栈顶弹出；
  - 如果不匹配，说明括号无效；
- 遍历完成后，如果栈为空，说明所有括号都正确配对，字符串有效；否则无效。

这种方式利用了栈「后进先出」的特性，非常适合用于匹配括号问题。

---


```python
def isValid(self, s: str) -> bool:
        parenthese_dict = {')':'(',']':'[','}':'{'}
        stack = []

        for ch in s:
            if ch not in parenthese_dict:
                stack.append(ch)
            else:
                if stack and parenthese_dict[ch] == stack[-1]:
                    stack.pop()
                else:
                    stack.append(ch)
        
        return len(stack) == 0
```
