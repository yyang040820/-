## 383 Ransom Note

题目链接:[https://leetcode.com/problems/ransom-note/description/]

Given two strings ransomNote and magazine, return true if ransomNote can be constructed by using the letters from magazine and false otherwise.

Each letter in magazine can only be used once in ransomNote.

 

Example 1:

Input: ransomNote = "a", magazine = "b"
Output: false
Example 2:

Input: ransomNote = "aa", magazine = "ab"
Output: false
Example 3:

Input: ransomNote = "aa", magazine = "aab"
Output: true
 

Constraints:

1 <= ransomNote.length, magazine.length <= 105
ransomNote and magazine consist of lowercase English letters.

#### 简洁回答
我们可以使用一个哈希表来优化对 ransomNote 是否可以由 magazine 构成的判断过程。核心思想是：统计 magazine 中每个字母的可用次数，并逐个匹配 ransomNote 的字母需求。

#### 详细回答
暴力解法是通过两层循环遍历 ransomNote 和 magazine，逐个查找并移除匹配字母，时间复杂度较高。

我们可以使用 HashMap（或 collections.Counter）优化：

#### 1. 预处理：首先统计 magazine 中每个字母的出现频率，存入一个哈希表中；

#### 2. 验证：遍历 ransomNote 中的每个字母，逐一消耗哈希表中对应的字母：

- 若该字母在哈希表中不存在，说明 magazine 中根本没有，返回 False；

- 若该字母频率为 0，说明已被消耗完；

- 否则，将该字母频率减一；

- 当某个字母频率减到 0，我们可以选择将其从哈希表中移除，以便之后快速判断是否还存在。

这种方式使得判断过程仅需 一次遍历 magazine 和一次遍历 ransomNote，时间复杂度为 O(m + n)，其中 m 和 n 分别是两个字符串的长度。

```python
def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        # record_ransom = Counter(ransomNote)
        record_magazine = Counter(magazine)

        for letter in ransomNote:
            if letter not in record_magazine:
                return False
            record_magazine[letter] -= 1
            if record_magazine[letter] == 0:
                del record_magazine[letter]
                
        return True
```
