## 111. Minimum Depth of Binary Tree


题目链接:[https://leetcode.com/problems/minimum-depth-of-binary-tree/description/]


题意：Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

Note: A leaf is a node with no children.


#### 简洁回答

可以使用 DFS 打擂台更新最小深度，也可以使用 BFS，在遇到第一个叶子节点时立即返回对应深度（更高效）。

---

#### 详细回答

本题有两种常见解法：

---

✅ **方法一：DFS（深度优先搜索）**

- 用递归遍历每条路径；
- 当遇到叶子节点时，尝试更新最小深度（打擂台）；
- 注意在递归前判断左右子节点是否为空，避免访问空节点；
- 最后返回全局最小深度。

优点：写法直观  
缺点：最坏情况下会遍历整棵树。

✅ **方法二：BFS（广度优先搜索）**
- 使用队列进行层序遍历；

- 每访问一层就将深度加一；

- 当遇到第一个叶子节点时立即返回当前深度；

- 这种方法在树比较大的情况下效率更高。

优点：一旦找到第一个叶子节点即可返回，效率高
缺点：需要额外的队列空间

---




```python
def minDepth(self, root: Optional[TreeNode]) -> int:
    if root == None:
        return 0

    res = float('inf')
    def minDepthHelper(root,count):
        nonlocal res
        if root.left == None and root.right == None:
            res = min(res,count+1)
            return

        if root.left != None:
            minDepthHelper(root.left,count+1)
        if root.right != None:
            minDepthHelper(root.right,count+1)
    
    minDepthHelper(root,0)
    return res

```

```python
def minDepth(self, root: Optional[TreeNode]) -> int:
        count = 0
        if root == None:
            return count
        
        queue = deque([])
        queue.appendleft(root)

        while queue:
            cur_length = len(queue)
            count += 1
            for _ in range(cur_length):
                pop_node = queue.pop()
                if pop_node.left == None and pop_node.right == None:
                    return count
                if pop_node.left:
                    queue.appendleft(pop_node.left)
                if pop_node.right:
                    queue.appendleft(pop_node.right)
        

        return count
```
