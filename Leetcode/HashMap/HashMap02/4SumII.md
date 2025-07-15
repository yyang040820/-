## 454. 4Sum II

题目链接:[https://leetcode.com/problems/4sum-ii/]

Given four integer arrays nums1, nums2, nums3, and nums4 all of length n, return the number of tuples (i, j, k, l) such that:

0 <= i, j, k, l < n
nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0
 

Example 1:

Input: nums1 = [1,2], nums2 = [-2,-1], nums3 = [-1,2], nums4 = [0,2]
Output: 2
Explanation:
The two tuples are:
1. (0, 0, 0, 1) -> nums1[0] + nums2[0] + nums3[0] + nums4[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> nums1[1] + nums2[1] + nums3[0] + nums4[0] = 2 + (-1) + (-1) + 0 = 0
Example 2:

Input: nums1 = [0], nums2 = [0], nums3 = [0], nums4 = [0]
Output: 1
 

Constraints:

n == nums1.length
n == nums2.length
n == nums3.length
n == nums4.length
1 <= n <= 200
-228 <= nums1[i], nums2[i], nums3[i], nums4[i] <= 228

#### 简洁回答
使用哈希表将四个数组分成两组分别求和，转化为“2Sum”问题，降低时间复杂度。最终统计所有满足条件的组合数。

#### 详细回答
题目要求从 四个不同的数组 中各取一个数，使得它们的和为目标值（例如 0）。暴力做法需要四重循环，时间复杂度为 O(n⁴)，效率极低。

我们可以通过分组和哈希表优化：

##### 1. 先处理前两个数组 nums1 和 nums2：

- 枚举所有可能的和，并统计每个和出现的次数。

- 使用一个哈希表 res_1 来存储这些和及其频率。

##### 2. 处理后两个数组 nums3 和 nums4：

- 同样枚举所有可能的和，但我们不是存储它们，而是计算 -(nums3[i] + nums4[j])。

- 查找这个值是否存在于之前的哈希表中，若存在，说明有组合可以凑成目标值（例如 0），将其频率加入计数器中。

这样整体时间复杂度从 O(n⁴) 降低到了 O(n²)，大大提升效率
```python
 def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
      res_1 = {}
      count = 0

      for i in range(len(nums1)):
          for j in range(len(nums2)):
              temp = nums1[i] + nums2[j]
              if temp in res_1:
                  res_1[temp] += 1
              else:
                  res_1[temp] = 1
      
      for i in range(len(nums3)):
          for j in range(len(nums4)):
              temp = -(nums3[i] + nums4[j])
              if temp in res_1:
                  count += res_1[temp]
                 
      return count
```
