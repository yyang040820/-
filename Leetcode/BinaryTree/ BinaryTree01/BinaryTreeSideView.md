## 199 Binary Tree Side View


题目链接:[https://leetcode.com/problems/binary-tree-right-side-view/description/]


题意：Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.




#### 简洁回答

使用 BFS（层序遍历）即可解决此问题。每层最先访问的节点即为该层的右视图节点，因此我们每层只记录第一个访问到的节点值。

---

#### 详细回答

此题的本质是**层序遍历 + 每层取最右边的节点**。

具体步骤如下：

1. 使用一个队列 `queue` 进行 BFS 层序遍历；
2. 遍历当前层时，**先将右子节点入队，再将左子节点入队**，这样每层最先访问的就是“最右边”的节点；
3. 对于每一层的第一个节点（即 `i == 0`），将其值加入结果列表 `res`；
4. 遍历完整棵树后，`res` 中即为右视图序列。

---




```python
def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        res = []
        if root == None:
            return res
        
        queue = deque([])
        queue.append(root)

        while queue:
            cur_length = len(queue)
            for i in range(cur_length):
                cur_node = queue.pop()
                if i == 0:
                    res.append(cur_node.val)
                if cur_node.right:
                    queue.appendleft(cur_node.right)
                if cur_node.left:
                    queue.appendleft(cur_node.left)
        
        return res

```
