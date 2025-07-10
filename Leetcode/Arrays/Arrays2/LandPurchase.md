## 开发商购买土地

#### 题目描述

在一个城市区域内，被划分成了n * m个连续的区块，每个区块都拥有不同的权值，代表着其土地价值。目前，有两家开发公司，A 公司和 B 公司，希望购买这个城市区域的土地。

现在，需要将这个城市区域的所有区块分配给 A 公司和 B 公司。

然而，由于城市规划的限制，只允许将区域按横向或纵向划分成两个子区域，而且每个子区域都必须包含一个或多个区块。

为了确保公平竞争，你需要找到一种分配方式，使得 A 公司和 B 公司各自的子区域内的土地总价值之差最小。

注意：区块不可再分。

【输入描述】

第一行输入两个正整数，代表 n 和 m。

接下来的 n 行，每行输出 m 个正整数。

输出描述

请输出一个整数，代表两个子区域内土地总价值之间的最小差距。

【输入示例】

3 3 \
1 2 3 \
2 1 3 \
1 2 3

【输出示例】

0

#### 回答
本题可以看作前缀和问题的衍生版，氛围横切或者竖切。无论是哪一种，首先我们按照1维的方法计算出相应的前缀和数组，然后寻找最小化(总和-2*子数组和)的绝对值。又由于不需要考虑部分切，因此只需要考虑总是从0位开端index即可。

```python
import sys
input = sys.stdin.read

def main():
    data = input().split()
    index = 0

    # Parse rows and cols from the first two tokens
    rows = int(data[index]);    index += 1
    cols = int(data[index]);    index += 1

    lands = []
    for _ in range(rows):
        # Read the next `cols` tokens and map them to ints
        row = list(map(int, data[index:index+cols]))
        lands.append(row)
        index += cols

    ans = float('inf')
    
    # Horizontally cut
    prefix_rows = [0] * rows
    for i in range(cols):
        prefix_rows[0] += lands[0][i]
    
    for j in range(1,rows):
        for i in range(cols):
            prefix_rows[j] += lands[j][i]
        prefix_rows[j] += prefix_rows[j-1]
    
    for i in range(rows):
        diff = abs(prefix_rows[rows-1] - 2 * prefix_rows[i])
        if diff < ans:
            ans = diff
        
    # Vertically cut
    prefix_cols = [0] * cols
    for i in range(rows):
        prefix_cols[0] += lands[i][0]
    
    for j in range(1,cols):
        for i in range(rows):
            prefix_cols[j] += lands[i][j]
        prefix_cols[j] += prefix_cols[j-1]
    
    for i in range(cols):
        diff = abs(prefix_cols[cols-1] - 2 * prefix_cols[i])
        if diff < ans:
            ans = diff
    
    print(ans)

if __name__ == "__main__":
    main()

```
