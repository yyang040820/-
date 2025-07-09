## 27. 移除元素

题目链接：[https://leetcode.cn/problems/remove-element/]

#### 简洁回答
为了在不使用额外空间的情况下从数组中移除指定数值并保持剩余元素的相对顺序，可以使用双指针法：一个指针 iterator 负责遍历数组，另一个指针 processed 指示下一个要覆盖的位置。当 iterator 指向的元素不是目标值时，将其赋值给 processed 所在位置，并同时移动两个指针；若是目标值，则仅移动 iterator。相比于使用额外数组的暴力解法（空间复杂度 O(n)），该方法实现了 O(1) 空间复杂度 的原地处理。

#### 详细回答
##### ✅ 题目解析与解法优化

本题要求从数组中**移除给定的数值**，并在此过程中**保持其余元素的相对索引顺序不变**。

##### 🚫 暴力解法

一种直接的思路是新建一个数组，只将不等于目标值的元素加入其中，最后用这个新数组覆盖原数组的内容。

- ✅ 简单易懂  
- ❌ 空间复杂度为 **O(n)**（其中 *n* 为原数组长度）

---

##### ✅ 原地移除 — 双指针法

为了节省空间，我们可以采用**同向双指针**策略，实现原地修改，空间复杂度为 **O(1)**。

定义两个指针：

- `processed`：表示已处理区间的末尾，所有 `0 ~ processed - 1` 的元素均为保留元素。
- `iterator`：遍历整个数组，查找下一个需要保留的元素。

##### 💡 操作逻辑

- 当 `iterator` 指向的是需要删除的元素：跳过，`iterator += 1`；
- 当 `iterator` 指向的是需要保留的元素：将该元素复制到 `processed` 指针的位置，然后 `processed += 1` 与 `iterator += 1` 同步前进。

这种方法可以在不使用额外空间的前提下，完成元素的原地覆盖。
```python
//暴力解法
def removeElement(self, nums: List[int], val: int) -> int:
        res = []
        count = 0
        for num in nums:
            if num != val:
                res.append(num)
                count += 1

        for i in range(count):
            nums[i] = res[i]
            
        return count
```

```python
//同向双指针解法
def removeElement(self, nums: List[int], val: int) -> int:
        processed = 0
        iterator = 0
        length = len(nums)

        while iterator < length:
            while iterator < length and nums[iterator] == val:
                iterator += 1
            
            if iterator < length:
                nums[processed] = nums[iterator]
                processed += 1
                iterator += 1
        
        return processed 
```
