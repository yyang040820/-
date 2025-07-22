## 145. Binary Tree Postorder Traversal

题目链接:[https://leetcode.com/problems/binary-tree-postorder-traversal/]

题意：Given the root of a binary tree, return the postorder traversal of its nodes' values. 


#### 简洁回答

本题是经典的**二叉树后序遍历**问题。后序遍历的顺序是：

> **左子树 → 右子树 → 根节点**

我们可以使用递归方式实现该遍历逻辑。

---

#### 详细回答

在后序遍历中，访问顺序如下：

1. 首先递归访问左子树；
2. 然后递归访问右子树；
3. 最后访问当前节点（根节点）。

递归函数中使用一个列表 `res` 来记录遍历结果，每次将当前节点值添加到末尾。该方法简单直观，适合作为后序遍历的入门实现。

---


```python
def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res = []

        def postorderHelper(cur):
            if cur == None:
                return
            postorderHelper(cur.left)
            postorderHelper(cur.right)
            res.append(cur.val)
        
        postorderHelper(root)
        return res

```
