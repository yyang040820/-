## 107. Binary Tree Level Order Traversal II

题目链接:[https://leetcode.com/problems/binary-tree-level-order-traversal-ii/description/]

题意： Given the root of a binary tree, return the bottom-up level order traversal of its nodes' values. (i.e., from left to right, level by level from leaf to root).

#### 详细回答

题目要求“**从下到上**”的层序遍历，但我们可以先正常执行“从上到下”的遍历，然后再将结果反转。实现过程如下：

1. 使用 `deque` 作为辅助队列，进行 BFS；
2. 每轮循环处理一整层节点，并记录该层所有节点的值；
3. 将每层的结果存入 `res` 列表；
4. 遍历完成后，使用 `res[::-1]` 进行翻转，得到自底向上的顺序。

注意事项：
- 虽然你原始代码中使用了 `appendleft` 和 `pop`，但这样会让逻辑变得混乱；
- 更清晰的做法是：使用 `popleft()` 正常从队列前端取出节点，并使用 `append()` 添加左右子节点。

---


```python
def levelOrderBottom(self, root: Optional[TreeNode]) -> List[List[int]]:
        res = []
        if root == None:
            return res
        queue = deque([])
        queue.appendleft(root)

        while queue:
            cur_length = len(queue)
            temp = []
            for _ in range(cur_length):
                cur_node = queue.pop()
                temp.append(cur_node.val)
                if cur_node.left:
                    queue.appendleft(cur_node.left)
                if cur_node.right:
                    queue.appendleft(cur_node.right)
            res.append(temp)
        
        # left = 0
        # right = len(res) - 1
        # while left < right:
        #     res[left],res[right] = res[right],res[left]
        #     left = left + 1
        #     right = right - 1

        return res[::-1]
```
