## 202 快乐数

题目链接:[https://leetcode.com/problems/happy-number/]

编写一个算法来判断一个数 n 是不是快乐数。

「快乐数」定义为：对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和，然后重复这个过程直到这个数变为 1，也可能是 无限循环 但始终变不到 1。如果 可以变为  1，那么这个数就是快乐数。

如果 n 是快乐数就返回 True ；不是，则返回 False 。

示例：

输入：19
输出：true
解释：
1^2 + 9^2 = 82
8^2 + 2^2 = 68
6^2 + 8^2 = 100
1^2 + 0^2 + 0^2 = 1

#### 简洁回答
本题通过不断计算数字的数位平方和，并利用哈希集合记录中间结果来判断是否进入循环。若最终结果为 1，则该数为快乐数；若中间结果重复，则不是快乐数。该方法高效且避免了无限循环。

#### 详细回答
本题的目标是判断一个数是否为快乐数。所谓快乐数，是指对一个正整数不断进行“各数位平方和”的计算，最终是否能够得到 1。如果某个中间结果重复出现，说明进入了循环，无法得到 1。

具体可以分为以下两步：

计算数位平方和：
1. 对当前数字进行逐位处理，可以使用除法（//10）和取模运算（%10）来提取每一位数字，并累加其平方，得到新的数字。

判断循环与终止条件：

1. 使用一个哈希集合（previous_res）记录已经出现过的平方和结果：

2. 如果某次结果为 1，说明是快乐数，返回 True；

  如果当前结果已出现在 seen 中，说明陷入循环，不是快乐数，返回 False；

  否则，将当前结果加入集合，继续下一轮平方和计算。

```python
def isHappy(self, n: int) -> bool:
    previous_res = set()
    previous_res.add(n)
    cur = n

    while True:
        square_sum = 0
        while cur // 10 > 0:
            square_sum += (cur % 10) * (cur % 10)
            cur = cur // 10

        square_sum += (cur % 10) * (cur % 10)

        if square_sum == 1:
            return True
        elif square_sum in previous_res:
            return False
        previous_res.add(square_sum)

        cur = square_sum
```
