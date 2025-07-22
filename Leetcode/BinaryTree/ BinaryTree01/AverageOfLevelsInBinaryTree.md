## 637. Average of Levels in Binary Tree


题目链接:[https://leetcode.com/problems/average-of-levels-in-binary-tree/description/]


题意：Given the root of a binary tree, return the average value of the nodes on each level in the form of an array. Answers within 10-5 of the actual answer will be accepted.


#### 简洁回答

使用广度优先搜索（BFS）逐层遍历树节点，计算每层节点值的平均数。

---

#### 详细回答

本题与标准的层序遍历类似，只是在遍历每层节点时额外计算节点值之和，遍历完该层后计算平均值并添加到结果列表中。

具体步骤：

1. 使用队列进行 BFS；
2. 遍历当前层所有节点，累计该层节点值之和；
3. 计算平均值（sum / 当前层节点数），加入结果；
4. 继续处理下一层，直到队列为空。

---




```python
def averageOfLevels(self, root: Optional[TreeNode]) -> List[float]:
        res = []
        queue = deque([])

        queue.appendleft(root)

        while queue:
            cur_length = len(queue)
            sum = 0
            for _ in range(cur_length):
                cur_node = queue.pop()
                sum += cur_node.val
                if cur_node.left:
                    queue.appendleft(cur_node.left)
                if cur_node.right:
                    queue.appendleft(cur_node.right)
            res.append(sum/cur_length)

        return res

```



