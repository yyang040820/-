## 区间和
题目描述

给定一个整数数组 Array，请计算该数组在每个指定区间内元素的总和。

输入描述

第一行输入为整数数组 Array 的长度 n，接下来 n 行，每行一个整数，表示数组的元素。随后的输入为需要计算总和的区间，直至文件结束。

输出描述

输出每个指定区间内元素的总和。

输入示例

5
1
2
3
4
5
0 1
1 3

#### 简洁回答
预先计算前缀和数组 `prefix_sum[i] = sum(nums[0..i])`，然后任意区间 `[start,end]` 的和可通过 `prefix_sum[end] - (start > 0 ? prefix_sum[start-1] : 0)` 在 O(1) 时间内获得，从而将单次查询从 O(n) 优化到 O(1)，总复杂度降为 O(n + m)，额外空间 O(n)。


#### 详细回答
假设数组长度为 \(n\)，需要回答 \(m\) 次区间和查询，**暴力**做法的时间复杂度为 \(O(m \times n)\)。由于数组元素不变，我们可以：

1. **构建前缀和数组**  
   - 新建长度为 \(n\) 的数组 `prefix_sum`。  
   - 对于每个索引 \(i\)（0-based），令  
     \[
       \text{prefix\_sum}[i]
         = \sum_{k=0}^{i} \text{nums}[k].
     \]
   - 也就是说 `prefix_sum[i]` 存储从数组开头到第 \(i\) 个元素（双端都包含）的子数组和。

2. **\(O(1)\) 时间回答任意区间 \([\,\text{start},\text{end}\,]\)**  
   - 若 \(\text{start}>0\)，则  
     \[
       \sum_{k=\text{start}}^{\text{end}} \text{nums}[k]
       = \text{prefix\_sum}[\text{end}] - \text{prefix\_sum}[\text{start}-1].
     \]
   - 若 \(\text{start}=0\)，直接取  
     \[
       \sum_{k=0}^{\text{end}} \text{nums}[k]
       = \text{prefix\_sum}[\text{end}].
     \]

通过预处理前缀和，整体时间复杂度降为 \(O(n + m)\)，空间额外使用 \(O(n)\)。


```python
import sys
input = sys.stdin.read
def main():
    data = input().split()
    index = 0
    n = int(data[index])
    index += 1
    nums = []
    for i in range(n):
        nums.append(int(data[index + i]))
    index += n

    prefix_sum = [0] * n
    prefix_sum[0] = nums[0]
    
    for i in range(1,n):
        prefix_sum[i] = prefix_sum[i-1] + nums[i]

    results = []
    while index < len(data):
        start = int(data[index])
        end = int(data[index + 1])
        index += 2

        if start == 0:
            sum_value = prefix_sum[end]
        else:
            sum_value = prefix_sum[end] - prefix_sum[start - 1]

        results.append(sum_value)

    for result in results:
        print(result)

if __name__ == "__main__":
    main()
```
