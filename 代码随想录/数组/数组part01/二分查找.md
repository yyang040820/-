## 704. 二分查找 

题目链接：[https://leetcode.cn/problems/binary-search/]

#### 简洁回答
1. **前提条件**：二分查找要求数组有序。

2. **常见区间写法**：
   - **左闭右闭**：`[left, right]`，循环条件 `while (left <= right)`
   - **左闭右开**：`[left, right)`，循环条件 `while (left < right)`

3. **语义区别**：
   - 左闭右闭：`right` 位置包含在搜索范围内。
   - 左闭右开：`right` 位置不包含在搜索范围内。

4. **初始化方式**：
   - 左闭右闭：`left = 0; right = len - 1`
   - 左闭右开：`left = 0; right = len`

5. **更新边界**（以 `target < nums[mid]` 为例）：
   - 左闭右闭：`right = mid - 1`
   - 左闭右开：`right = mid`

6. **常见错误**：
   - 左闭右开写法下初始化 `right = len - 1` 会漏掉最后一个元素。

#### 详细回答

##### 二分查找的基本原理与区间选择

二分查找的基本前提是：**目标序列必须是有序的**，这样才能利用中间值与目标值之间的大小关系来缩小搜索范围。通过比较目标值与中间值的关系，我们可以决定舍弃左半部分还是右半部分，从而不断收缩区间，最终定位目标。

二分查找的实现方式主要有两种：

- **左闭右闭区间**：`[left, right]`
- **左闭右开区间**：`[left, right)`

##### 区间含义

我的理解是：

- 对于**左闭右闭**的写法，可以认为**左指针左边**和**右指针右边**的元素都已经处理完了。
- 对于**左闭右开**的写法，由于右边是开区间，因此**右指针指向的位置本身不包含在搜索范围内**。

举个例子：

- 在左闭右闭下，区间 `[1, 1]` 是合法的，包含 index `1`。
- 在左闭右开下，区间 `[1, 1)` 是空集，表示搜索已经结束。

---

##### 初始化指针

因此，我们在初始化左右指针时应当注意：

- **左闭右闭**：`left = 0`，`right = len(nums) - 1`
- **左闭右开**：`left = 0`，`right = len(nums)`

> 如果在使用左闭右开的写法时却错误地将 `right` 初始化为 `len(nums) - 1`，那么最后一个元素就不会被纳入搜索范围，从而可能导致错误结果。

---

##### 应用在本题中的逻辑

在本题中，数组是**升序排列**的，我们使用的是**左闭右闭**的写法。因此：

- 左指针 `left` 指向下界（lower bound），右指针 `right` 指向上界（upper bound）。
- 如果目标值 `target > nums[mid]`，说明目标在右半部分，更新左边界：`left = mid + 1`。
- 如果目标值 `target < nums[mid]`，说明目标在左半部分，更新右边界：
  - 在左闭右闭下：`right = mid - 1`
  - 在左闭右开下：`right = mid`


```python
// 左闭右闭
def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1
        while left <= right:
            mid = left + (right - left) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] > target:
                right = mid - 1
            else:
                left = mid + 1
        return -1
```

```python
// 左闭右开
def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums)
        while left < right:
            mid = left + (right - left) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] > target:
                right = mid
            else:
                left = mid + 1
        return -1
```


#### 知识拓展
后续将更新关于lower bound和upper bound的延展性二分法理解
