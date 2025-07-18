## Implement Queue using Stacks
题目链接:[https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/description/]

题意： 
You are given a string s consisting of lowercase English letters. A duplicate removal consists of choosing two adjacent and equal letters and removing them.

We repeatedly make duplicate removals on s until we no longer can.

Return the final string after all such duplicate removals have been made. It can be proven that the answer is unique.

 

Example 1:

Input: s = "abbaca"
Output: "ca"
Explanation: 
For example, in "abbaca" we could remove "bb" since the letters are adjacent and equal, and this is the only possible move.  The result of this move is that the string is "aaca", of which only "aa" is possible, so the final string is "ca".
Example 2:

Input: s = "azxxzy"
Output: "ay"
 

Constraints:

1 <= s.length <= 105
s consists of lowercase English letters.

#### 简洁回答
使用栈（Stack）结构可以高效地删除相邻的重复字母。遍历字符串时，若当前字符与栈顶字符相同，则将栈顶元素弹出；否则，将当前字符压入栈中。最终将栈中字符连接返回即可。
  
#### 详细回答

要删除相邻的重复字母，我们可以利用栈结构的特性：栈的顶部元素始终是上一个字符，因此非常适合用于比较当前字符与前一个字符是否重复。

遍历字符串时：
- 如果栈不为空，检查当前字符是否等于栈顶字符。
  - 若相等，说明出现了相邻重复字符，将栈顶元素弹出。
  - 若不相等，则将当前字符压入栈中。
- 如果栈为空，直接压入当前字符。


```python
def removeDuplicates(self, s: str) -> str:
        stack = []

        for ch in s:
            if stack:
                top = stack[-1]
                if top == ch:
                    stack.pop()
                    continue
            stack.append(ch)
              
        return ''.join(stack)
```
