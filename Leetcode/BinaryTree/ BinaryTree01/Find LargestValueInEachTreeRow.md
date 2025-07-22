## 515. Find Largest Value in Each Tree Row

题目链接:[https://leetcode.com/problems/find-largest-value-in-each-tree-row/description/]

题意：Given the root of a binary tree, return an array of the largest value in each row of the tree (0-indexed).

#### 简洁回答

使用广度优先搜索（BFS）逐层遍历，记录每层节点的最大值。

---

#### 详细回答

思路：

1. 使用队列进行层序遍历（BFS）；
2. 对每层所有节点进行遍历，维护该层最大值 `temp`；
3. 当前层遍历完成后，将最大值加入结果列表；
4. 继续遍历下一层，直到队列为空。

---



```python
def largestValues(self, root: Optional[TreeNode]) -> List[int]:
      res = []
      if root == None:
          return res
      
      queue = deque([])
      queue.appendleft(root)

      while queue:
          cur_length = len(queue)
          temp = -float('inf')
          for _ in range(cur_length):
              cur_node = queue.pop()
              temp = max(cur_node.val,temp)
              if cur_node.left:
                  queue.appendleft(cur_node.left)
              if cur_node.right:
                  queue.appendleft(cur_node.right)
          res.append(temp)
      
      return res

```
