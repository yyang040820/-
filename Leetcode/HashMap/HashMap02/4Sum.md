## 18.4 Sum

题目链接:[https://leetcode.com/problems/4sum/description/]
Given an array nums of n integers, return an array of all the unique quadruplets [nums[a], nums[b], nums[c], nums[d]] such that:

0 <= a, b, c, d < n
a, b, c, and d are distinct.
nums[a] + nums[b] + nums[c] + nums[d] == target
You may return the answer in any order.

 

Example 1:

Input: nums = [1,0,-1,0,-2,2], target = 0
Output: [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
Example 2:

Input: nums = [2,2,2,2,2], target = 8
Output: [[2,2,2,2]]
 

Constraints:

1 <= nums.length <= 200
-109 <= nums[i] <= 109
-109 <= target <= 109

#### 简洁回答
Four Sum 问题与 Three Sum、Two Sum 类似，关键在于：避免重复 和 合理剪枝。我们可以使用 Counter 来统计每个数字出现的次数，并用三重循环构建前三个数，最后判断第四个数是否满足条件，且未超出频率限制。

#### 详细回答
与 Three Sum 类似，Four Sum 的目标是找出所有不重复的四元组 [a, b, c, d]，使得 a + b + c + d == target。

暴力解法为四层嵌套循环，时间复杂度为 $O(n^4)$，但我们可以通过以下方式做一些优化：

#### 解法核心：
1. 使用 collections.Counter 统计 nums 中每个元素出现的频率；

2. 使用三重循环确定前三个数 (nums[i], nums[j], nums[k])；

3. 计算出第4个数 val = target - (i + j + k)；

4. 检查 val 是否在 Counter 中；

- 如果存在，还需判断该数是否被过度使用（即已在前三个数中出现过几次）；
  
5. 使用 set 存储排好序的四元组，确保最终结果不重复；

6. 最后将 set 中的 tuple 转换为 list 返回
   
```python
def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        count_map = Counter(nums)
        size = len(nums)
        res = set()

        for i in range(size):
            for j in range(i+1,size):
                for m in range(j+1,size):
                    val = target - (nums[i] + nums[j] + nums[m])
                    if val in count_map:
                        count = (val == nums[i]) + (val == nums[j]) + (val == nums[m])
                        if count_map[val] > count:
                            res.add(tuple(sorted([nums[i],nums[j],nums[m],val])))

        return [list(x) for x in res]
```
