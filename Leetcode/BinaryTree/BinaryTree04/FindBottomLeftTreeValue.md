## 513 Find Bottom Left Tree Value

题目链接:[https://leetcode.com/problems/find-bottom-left-tree-value/description/]

题意： Given the root of a binary tree, return the leftmost value in the last row of the tree.


#### ✅ 简洁回答

可以使用 **层序遍历** 找到最后一层的最左节点，或者使用 **递归** 并结合深度打擂台的方式记录最深处的最左节点。

---

#### 🔍 详细解析

我们有两种常见做法来解决这个问题：

##### 方法一：层序遍历（BFS）

- 每次遍历一层节点；
- 每层的第一个节点就是当前层最左的节点；
- 最后一层第一个节点即为答案。


##### 方法二：递归（DFS 打擂台）
- 用递归遍历整棵树；

- 每次遇到叶子节点，判断其深度是否大于当前记录的最大深度；

- 如果是，则更新结果；

- 因为是先遍历左子树，所以天然保证最左优先，无需额外标记。

```python
def findBottomLeftValue(self, root: Optional[TreeNode]) -> int:
        res = root.val
        queue = deque([])
        queue.appendleft(root)

        while queue:
            cur_length = len(queue)
            for i in range(cur_length):
                cur_node = queue.pop()
                if i == 0:
                    res = cur_node.val
                if cur_node.left:
                    queue.appendleft(cur_node.left)
                if cur_node.right:
                    queue.appendleft(cur_node.right)

        return res 
```

```python
def findBottomLeftValue(self, root: Optional[TreeNode]) -> int:
        max_depth = 0
        res = root.val
        
        def findBottomLeftValueHelper(root,depth):
            nonlocal max_depth
            nonlocal res
            if root == None:
                return
            
            if root.left == None and root.right == None:
                if depth > max_depth:
                    max_depth = depth
                    res = root.val

            
            findBottomLeftValueHelper(root.left,depth+1)
            findBottomLeftValueHelper(root.right,depth+1)
        
        findBottomLeftValueHelper(root,0)

        return res
```
