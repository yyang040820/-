## 429. N-ary Tree Level Order Traversal 

题目链接:[https://leetcode.com/problems/n-ary-tree-level-order-traversal/description/]


题意：Given an n-ary tree, return the level order traversal of its nodes' values.

Nary-Tree input serialization is represented in their level order traversal, each group of children is separated by the null value (See examples).




#### 简洁回答

使用队列进行广度优先搜索（BFS），遍历每层所有节点，并依次访问所有子节点。

---

#### 详细回答

与二叉树层序遍历类似，区别在于：

- 每个节点可能有多个子节点，存储在 `children` 列表中；
- 遍历时需遍历所有子节点并加入队列。

遍历过程中：

1. 用队列存储当前层节点；
2. 遍历当前层所有节点，收集它们的值；
3. 将当前节点的所有子节点加入队列，供下一层遍历；
4. 重复上述步骤，直到队列为空。

---



```python
def levelOrder(self, root: 'Node') -> List[List[int]]:
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
                for child in cur_node.children:
                    queue.appendleft(child)
            res.append(temp)
        
        return res
```
