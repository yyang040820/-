## 59.螺旋矩阵II

题目链接：https://leetcode.cn/problems/spiral-matrix-ii/

#### 简洁回答
逐圈填充思路直观易懂，适合明确层次结构；动态转向方法代码更简洁，只需维护当前位置和方向数组，无需额外计算圈数，两者时间复杂度均为 O(m·n)，空间复杂度 O(1)。

#### 详细回答
本题要求以横向与纵向的“螺旋”顺序填充数字，关键在于何时改变填充方向。常见的两种思路：

1. **逐圈填充**  
   - 按圈数依次处理：第 1 圈、第 2 圈…直到最外层；  
   - 对于每一圈，从其起始点出发，依次向右、向下、向左、向上填充；  
   - 总圈数为 `min(m, n) / 2`（向下取整），如果 `min(m, n)` 为奇数，还需额外在中心单独处理最后一格。

2. **动态转向**  
   - 不预先计算圈数，仅维护当前坐标 `(i, j)` 和方向数组 `dirs = [(0,1),(1,0),(0,-1),(-1,0)]`（分别表示右、下、左、上）；  
   - 每步尝试按当前方向前进一步，若越界或该位置已填，则“转弯”：`dir = (dir + 1) % 4`，再沿新方向前进；  
   - 重复直到所有格子填满。

> **转向判断**：  
> - 下一步行或列索引超出边界；  
> - 或者该格已被赋值。  
> 此时执行 `dir = (dir + 1) % 4`，再移动。

```python
//逐圈填写
def generateMatrix(self, n: int) -> List[List[int]]:
        res = [[0] * n for _ in range(n)]
        loops = n // 2

        start_row = 0
        start_col = 0
        end_row = n - 1
        end_col = n - 1
        loops_count = 0
        count = 0
        total = n * n
        
        while loops_count < loops:
            res[start_row][start_col] = count + 1
            count = count + 1
            # Right
            for i in range(start_col + 1,end_col+1):
                res[start_row][i] = count + 1
                count = count + 1
            # Down
            for i in range(start_row + 1,end_row+1):
                res[i][end_col] = count + 1
                count = count + 1
            # Left
            for i in range(end_col-1,start_col-1,-1):
                res[end_row][i] = count + 1
                count = count + 1
            # Up
            for i in range(end_row-1,start_row,-1):
                res[i][start_col] = count + 1
                count = count + 1

            loops_count += 1
            start_row += 1
            start_col += 1
            end_row -= 1
            end_col -= 1
        
        if n % 2 == 1:
            res[start_row][start_col] = count + 1
            count = count + 1


        return res
```

```python
def generateMatrix(self, n: int) -> List[List[int]]:
        res = [[0]*n for _ in range(n)]
        print(res)
        directions = [[0,1],[1,0],[0,-1],[-1,0]]
        cur_direction_index = 0
        cur_row = 0
        cur_col = 0
        total = n * n

        for i in range(total):
            res[cur_row][cur_col] = i+1
            attempted_row = cur_row + directions[cur_direction_index][0]
            attempted_col = cur_col + directions[cur_direction_index][1]
            

            if attempted_row < 0 or attempted_row >= n or attempted_col < 0 or attempted_col >= n or res[attempted_row][attempted_col] != 0:
                cur_direction_index = (cur_direction_index + 1)% 4
                cur_row = cur_row + directions[cur_direction_index][0]
                cur_col = cur_col + directions[cur_direction_index][1]
            else:
                cur_row = attempted_row
                cur_col = attempted_col
            
        
        return res
```
