## 242.有效的字母异位词 

题目链接:[https://leetcode.com/problems/valid-anagram/]

给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。

示例 1: 输入: s = "anagram", t = "nagaram" 输出: true

示例 2: 输入: s = "rat", t = "car" 输出: false

#### 简洁回答
通过先统计第一个单词的字母频数，再逐一匹配第二个单词中的字母，可以高效判断两个单词是否为字母异位词，无需额外的空间来记录第二个单词的频数。

#### 详细回答
在判断两个单词是否为有效的字母异位词时，我们只需比较它们各自的字母及其出现次数是否完全一致。虽然可以使用两个字典分别统计两个单词中的字母频数，但我们也可以采用更高效的方法：先记录第一个单词的字母及其频数，然后遍历第二个单词进行匹配验证。如果某个字母不在字典中，或其出现次数超过原字典的记录，就说明这两个单词不是有效的异位词。

具体步骤如下：

1. 使用一个字典统计第一个单词中每个字母的出现频数；

遍历第二个单词：

1. 如果当前字母存在于字典中，则将对应频数减 1；

2. 若某个字母频数减为 0，则将其从字典中删除；

3. 若当前字母不在字典中，立即返回 False；

4. 如果整个遍历过程顺利完成，说明两个单词是有效的异位词，返回 True。



```python
def isAnagram(self, s: str, t: str) -> bool:
        record_first = {}

        for ch in s:
            if ch not in record_first:
                record_first[ch] = 1
            else:
                record_first[ch] += 1

        for ch in t:
            if ch not in record_first:
                return False
            else:
                record_first[ch] -= 1
                if record_first[ch] == 0:
                    del record_first[ch]
        
        return len(record_first) == 0
```
