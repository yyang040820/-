## 239. Sliding Window Maximum

题目链接:[https://leetcode.com/problems/sliding-window-maximum/description/]

题意： 
You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.

Example 1:

Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation: 
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
Example 2:

Input: nums = [1], k = 1
Output: [1]
 

Constraints:

1 <= nums.length <= 105
-104 <= nums[i] <= 104
1 <= k <= nums.length


#### 简洁回答
使用双端队列维护当前窗口的索引，保证队列中的元素对应的值单调递减；滑动时添加新元素、剔除过期索引，时间复杂度 O(N)。

#### 详细回答
本题要求对长度为 N 的数组 `nums`，以大小为 K 的滑动窗口依次计算每个窗口中的最大值。  
- **暴力方法**：每次滑动都在窗口内扫描一次，耗时 O(N·K)。  
- **优化思路**：利用双端队列（deque）维护“候选最大值索引”，并保证：
  1. **单调性**：队列从头到尾对应的 `nums` 值严格递减，新进元素时不断弹出队尾不大于它的索引；  
  2. **有效性**：队头索引若超出当前窗口范围 `[i-K+1, i]`，则弹出队头。  

这样，每个元素最多进出队列一次，整体时间复杂度降至 O(N)。

```python
from collections import deque
from typing import List

def maxSlidingWindow(nums: List[int], k: int) -> List[int]:
    dq = deque()   # 存放索引，保证对应值单调递减
    res = []

    # 初始化第一个窗口
    for i in range(k):
        while dq and nums[dq[-1]] <= nums[i]:
            dq.pop()
        dq.append(i)
    res.append(nums[dq[0]])

    # 滑动窗口
    for i in range(k, len(nums)):
        # 弹出窗口外的索引
        if dq and dq[0] == i - k:
            dq.popleft()
        # 保持单调递减
        while dq and nums[i] >= nums[dq[-1]]:
            dq.pop()
        dq.append(i)
        res.append(nums[dq[0]])

    return res
