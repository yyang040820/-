## 349. 两个数组的交集

题目链接: [https://leetcode.com/problems/intersection-of-two-arrays/]
题意：给定两个数组，编写一个函数来计算它们的交集（共同出现的字母）。

#### 简洁回答
通过将第一个数组元素存入哈希集合，并遍历第二个数组判断是否存在于集合中，可以高效求得两个数组的交集，最终以列表形式返回。该方法时间复杂度较低，适用于去重后的交集判断场景。

#### 详细回答
为了判断两个数组的交集，我们可以利用哈希集合（HashSet）提高查找效率。具体实现思路如下：

使用一个哈希集合（set_1）记录第一个数组中出现的所有元素；

初始化一个结果集合（res）用于存储交集结果；

遍历第二个数组中的每个元素：

如果该元素既存在于 set_1 中，又未被加入过 res，则将其添加到 res 中；

最后将 res 转换为列表返回，即为两个数组的交集。

```python
def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
      set_1 = set(nums1)
      res = set()

      for element in nums2:
          if element in set_1:
              res.add(element)
      
      return list(res)
```
