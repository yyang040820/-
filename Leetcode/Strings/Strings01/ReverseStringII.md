## 541.Reverse String II

题目链接:[https://leetcode.com/problems/reverse-string-ii/description/]

Given a string s and an integer k, reverse the first k characters for every 2k characters counting from the start of the string.

If there are fewer than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and leave the other as original.

 

Example 1:

Input: s = "abcdefg", k = 2
Output: "bacdfeg"
Example 2:

Input: s = "abcd", k = 2
Output: "bacd"
 

Constraints:

1 <= s.length <= 104
s consists of only lowercase English letters.
1 <= k <= 104

#### 简洁回答

本题要求以每 `2k` 个字符为一个窗口，对前 `k` 个字符进行反转：
- 若剩余字符少于 `k`，则反转所有剩余字符；
- 若剩余字符不少于 `k` 但不足 `2k`，只反转前 `k` 个字符，其余保持原样。

---

#### 详细回答
解题思路如下：

1. 将字符串 `s` 转为 `list`，因为 Python 字符串是 **不可变类型（immutable）**，无法原地修改；
2. 使用每步大小为 `2k` 的滑动窗口遍历整个字符串；
3. 在每个窗口中，仅对前 `k` 个字符进行反转；
4. 为防止越界，需要判断实际可以反转的终止位置是否超过字符串末尾；
5. 最终将列表重新拼接成字符串返回。

```python
def reverseStr(self, s: str, k: int) -> str:
        s = list(s)
        size = len(s)
        
        for start in range(0,size,2*k):
            temp = start + k - 1
            end = size - 1
            if temp < size - 1:
                end = temp
            self.reverserHelper(s,start,end)
            
        s = ''.join(s)
        return s  

    def reverserHelper(self,s,start,end):
        left = start
        right = end

        while left < right:
            temp = s[left]
            s[left] = s[right]
            s[right] = temp
            left = left + 1
            right = right - 1

```
