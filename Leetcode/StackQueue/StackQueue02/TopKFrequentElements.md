## 347. Top K Frequent Element

题目链接:[https://leetcode.com/problems/top-k-frequent-elements/description/]

题意： Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

Example 1:

Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
Example 2:

Input: nums = [1], k = 1
Output: [1]
 

Constraints:

1 <= nums.length <= 105
-104 <= nums[i] <= 104
k is in the range [1, the number of unique elements in the array].
It is guaranteed that the answer is unique.
 

Follow up: Your algorithm's time complexity must be better than O(n log n), where n is the array's size.


#### 简洁回答
先用哈希表统计所有元素的出现频率，再维护一个大小为 k 的最小堆，遍历频率表时将频率最低的元素踢出堆，最终堆中即为前 k 个高频元素。整体时间复杂度 O(N log k)。

#### 详细回答
本题需要在数组 `nums` 中找出出现频率最高的 k 个元素，思路如下：

1. **统计频率**  
   使用 `Counter`（或普通字典）一次遍历统计每个元素出现的次数，得到一个 `frequency_map`，时间 O(N)。

2. **维护大小为 k 的最小堆**  
   - 堆中存储元组 `(频率, 元素)`，堆顶始终是当前堆内频率最小的元素。  
   - 遍历 `frequency_map` 的每个 `(num, freq)`：  
     - 若堆中元素少于 k 个，直接 `heappush`；  
     - 否则比较当前频率与堆顶频率，若更大，则先 `heappop` 再 `heappush`，保证堆内始终是前 k 高频元素。  
   - 整体维护堆的操作为 O(M log k)，其中 M 是不同元素的个数，M ≤ N。

3. **输出结果**  
   遍历堆中元素，收集对应的数字即可。

> **可选优化**：也可以将所有 `(频率, 元素)` 放入数组，使用 Quickselect 在平均 O(N) 时间内选出前 k 大的前缀，然后直接截取，不借助额外空间。但堆方法已足够高效且易实现。


---


```python
def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        heap = []
        frequency_map = Counter(nums)
        size = len(nums)
        ans = []

        count = 0
        for key in frequency_map.keys():
            if count < k:
                heap.append((frequency_map[key],key))
                count += 1
            else:
                if count == k:
                    heapq.heapify(heap)
                heapq.heappush(heap,(frequency_map[key],key))
                heapq.heappop(heap)
                count += 1
        
        for ele in heap:
            ans.append(ele[1])
        
        return ans
```
