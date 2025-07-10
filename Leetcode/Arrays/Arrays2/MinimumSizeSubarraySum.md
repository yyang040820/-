## 209.长度最小的子数组
题目链接：https://leetcode.com/problems/minimum-size-subarray-sum/

#### 简洁回答
滑动窗口是解决本题的最佳方案：利用左右指针维护一个可增可缩的区间，在保证子数组和 ≥ 目标值的前提下不断收缩左端以更新最短长度，时间复杂度 O(n)、空间 O(1)。虽然基于前缀和 + 二分查找也能找到每个起点的最短终点，但其 O(n log n) 的时间和额外 O(n) 的空间开销通常不及滑动窗口高效。

#### 详细回答
本题要求找到最短的子数组长度，不难想到使用滑动窗口技巧。具体思路如下：

1. **滑动窗口**  
   - 使用左右指针构成一个闭区间 `[left, right]`。  
   - 首先不断将右指针 `right` 向右移动，直到当前窗口的元素和 ≥ 目标值；  
   - 随后移动左指针 `left`，在保证窗口和仍然 ≥ 目标值的前提下，持续缩小窗口；  
   - 在上述过程中，动态计算并更新最小窗口长度。  

由于题目中所有数字均为非负数，前缀和数组必然是单调递增的。这使得我们可以使用**二分查找**来优化查找每个起点对应的最小结束位置：

2. **二分查找**  
   - 预先构建前缀和数组 `prefixSum`；  
   - 对于每个起点 `i`，在 `prefixSum` 中查找最小的 `j` 使得 `prefixSum[j] - prefixSum[i] + nums[i] ≥ 目标值`；  
   - 记录所有起点对应的最短区间长度，再取全局最小。  

> **注意**：二分查找方法虽然思想清晰，但时间复杂度为 `O(n log n)`，并且需要额外的 `O(n)` 空间来存储前缀和，整体性能通常不及滑动窗口的 `O(n)`。  



```python
//双指针。时间复杂度:O(n);空间复杂度:O(1),n为数组长度
def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        left = 0
        size = len(nums)
        res = size + 1 # It is not possible to be longer than the length of the array
        cur = 0

        for right in range(size):
            cur += nums[right]

            while cur >= target:
                temp_len = right - left + 1
                if temp_len < res:
                    res = temp_len
                cur -= nums[left]
                left = left + 1
        
        if res <= size:
            return res
        else:
            return 0
```

```python
//前缀和+Binary Search。时间复杂度O(nlogn);空间复杂度:O(n)
def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        presum = []
        size = len(nums)
        cur = 0
        ans = size + 1

        for i in range(size):
            presum.append(cur + nums[i])
            cur = presum[-1]
        
        for i in range(size):
            left = i
            right = size - 1
            
            # Find the lower bound
            while left <= right:
                mid = left + (right - left) //2
                # Calculate the subarray sum from i to mid
                subSum = presum[mid] - presum[i] + nums[i]
                if subSum >= target:
                    ans = min(mid - i + 1,ans)
                    right = mid - 1
                else:
                    left = mid + 1
        
        if ans <= size:
            return ans
        else:
            return 0
```
