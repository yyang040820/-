## 102 Binary Tree Level Order Traversal

题目链接:[https://leetcode.com/problems/binary-tree-level-order-traversal/]

题意： Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).


#### 简洁回答

使用**队列（Queue）**进行广度优先搜索（BFS），每次处理一层的所有节点，同时将下一层的节点加入队列中，最终得到每层的节点值列表。

---

#### 详细回答

**层序遍历（Level Order Traversal）**是一种广度优先搜索（BFS）策略。我们通过以下步骤来实现：

1. 使用一个队列（`deque`）来辅助遍历，初始时将根节点加入队列；
2. 每次从队列中取出当前层的所有节点，并记录它们的值；
3. 对于每个节点，将其左右子节点加入队列（用于下一层的遍历）；
4. 重复此过程直到队列为空。

注意：
- Python 的 `collections.deque` 支持高效地从队列两端插入或删除元素；
- 本题中为了保持从左到右的顺序，应使用 `popleft()` 从左边取元素，同时使用 `append()` 将子节点加到队列右端。

---


```python
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        res = []
        if root == None:
            return res
        queue = deque([])
        queue.append(root)
        

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
        
        return res
```
