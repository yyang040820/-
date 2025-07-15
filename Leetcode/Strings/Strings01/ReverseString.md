## 344.Reverse String

题目链接:[https://leetcode.com/problems/reverse-string/description/]
Write a function that reverses a string. The input string is given as an array of characters s.

You must do this by modifying the input array in-place with O(1) extra memory.

Example 1:

Input: s = ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
Example 2:

Input: s = ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]

#### 简洁回答
使用左右指针交换字符，逐步向中间收缩，即可实现原地反转。由于输入是 `List[str]`，可以直接修改。如果输入是 `str` 类型，由于其不可变性，需先转换为列表再操作。

---

#### 详细回答
要反转字符串列表，我们可以使用两个指针，一个从左开始，一个从右开始，每次交换两个指针所指的字符，并将指针向中间移动，直到相遇。

关键点：
- 输入是 `List[str]`，是可变对象，支持原地修改；
- 如果输入是字符串（`str` 类型），由于字符串在 Python 中是不可变的，就不能用下标赋值，必须先转换为 `list`，反转后再用 `''.join()` 拼回字符串。

---
```python
def reverseString(self, s: List[str]) -> None:
    """
    Do not return anything, modify s in-place instead.
    """
    size = len(s)
    left = 0
    right = size - 1

    while left < right:
        temp = s[left]
        s[left] = s[right]
        s[right] = temp
        left = left + 1
        right = right - 1

```
