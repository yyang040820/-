## 977.有序数组的平方 

题目链接：[https://leetcode.com/problems/squares-of-a-sorted-array/]

#### 简洁回答
本题要求将有序数组中的元素平方后重新按升序排列。暴力解法是先平方再排序，时间复杂度为 O(nlogn)。但由于原数组有序，我们可以用双指针法在线性时间内完成。具体做法是从两端同时比较绝对值较大的元素，将其平方并从结果数组的末尾开始填入，最终得到一个升序的平方数组，整体时间复杂度为 O(n)，空间复杂度为 O(n)。

#### 详细回答
本题要求将一个**有序数组中的元素平方后**，按**从小到大**的顺序重新排列。

---

##### 🚫 暴力解法

最直接的做法是：
1. 将数组中每个元素平方；
2. 然后对整个新数组进行排序。

这种方式的时间复杂度为 **O(n log n)**，未能充分利用原数组已经有序的特性。

---

##### ✅ 双指针优化 — 时间复杂度 O(n)

由于原数组是升序排列的，负数平方后可能比正数还大，例如 `-100` 和 `1`，平方后分别是 `10000` 和 `1`，所以最大值可能出现在数组的两端。

##### ✅ 解法核心思路：

- 使用两个指针 `left` 和 `right`，分别指向数组的两端。
- 每次比较 `abs(nums[left])` 和 `abs(nums[right])`：
  - 如果左边更大，将其平方后放入结果数组的末尾，然后 `left + 1`；
  - 否则将右边的平方插入结果末尾，`right - 1`。
- 从后往前填充结果数组，保证是按从大到小插入，再反转或从后向前填充即为升序。

---


```python
    def sortedSquares(self, nums: List[int]) -> List[int]:
        left = 0
        right = len(nums) - 1
        res = [0] * len(nums)
        count = len(nums) - 1

        while count >= 0:
            if abs(nums[left]) >= abs(nums[right]):
                res[count] = nums[left] * nums[left]
                left = left + 1
            else:
                res[count] = nums[right] * nums[right]
                right = right - 1
            count = count - 1

        return res
```
