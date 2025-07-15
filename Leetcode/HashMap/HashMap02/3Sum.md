## 15. 3Sum

题目链接:[https://leetcode.com/problems/3sum/description/]
Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

 

Example 1:

Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.
Example 2:

Input: nums = [0,1,1]
Output: []
Explanation: The only possible triplet does not sum up to 0.
Example 3:

Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only possible triplet sums up to 0.
 

Constraints:

3 <= nums.length <= 3000
-105 <= nums[i] <= 105

#### 简洁回答
threeSum 问题要求找出所有不重复的三元组 [a, b, c]，使得 a + b + c = 0。暴力解法时间复杂度为 $O(n^3)$，可以通过排序 + 双指针或哈希集合优化为 $O(n^2)$。

#### 详细回答
暴力解法是三层嵌套循环遍历所有三元组组合，效率低下。

优化方法：

首先对数组进行排序，这样我们可以：

快速跳过重复值；

使用双指针策略。

##### 方法一：使用 HashSet（基于 2Sum 的哈希解法）
1. 固定第一个数 nums[i]，问题转为在 nums[i+1:] 中找两个数之和为 -nums[i]。

2. 使用 HashSet 存储当前扫描过的数，用于查找目标值。

3. 为避免重复三元组，遍历时跳过相邻重复元素。

##### 方法二：双指针解法（排序 + 双指针）
1. 固定 nums[i] 后，在 nums[i+1:] 范围内使用双指针查找 target = -nums[i]。

2. 排序后，可以高效跳过重复元素。

3. 左右指针收缩，直到满足条件或指针相遇。需要注意的是，在凑够数之后，我们还要把左指针和右指针同时收缩，因为还有可能后续有其它答案。

```python
//用hashset来处理
def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        res = []
        size = len(nums)
        for i in range(len(nums)):
            if nums[i] > 0:
                break
            if i >= 1 and nums[i-1] == nums[i]:
                continue
            target = - nums[i]
            seen = set()
            j = i + 1
            while j < size:
                if target - nums[j] in seen:
                    res.append([nums[i],nums[j],target - nums[j]])
                    while j + 1 < size and nums[j] == nums[j+1]:
                        j = j + 1
                seen.add(nums[j])
                j = j + 1        
        return res
```

```python
//双指针
def threeSum(self, nums: List[int]) -> List[List[int]]:
      nums.sort() # O(nlogn)
      size = len(nums)
      res = []

      # O(n^2)
      for i in range(len(nums)):
          if i >= 1 and nums[i] == nums[i-1]:
              continue
          target = - nums[i]
          left = i + 1
          right = size - 1

          while left < right:
              if left != i + 1 and right != size - 1:
                  if nums[left] == nums[left-1] or nums[right] == nums[right+1]:
                      if nums[left] == nums[left-1]:
                          left = left + 1
                      if nums[right] == nums[right+1]:
                          right = right - 1
                      continue

              temp = nums[left] + nums[right]
              if temp == target:
                  res.append([nums[i],nums[left],nums[right]])
                  left = left + 1
                  right = right - 1
              elif temp < target:
                  left = left + 1
              else:
                  right = right - 1
      
      return res
```
