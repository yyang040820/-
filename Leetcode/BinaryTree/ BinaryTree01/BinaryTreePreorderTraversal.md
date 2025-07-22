## 144. Binary Tree Preorder Traversal.md

题目链接:[https://leetcode.com/problems/binary-tree-preorder-traversal/description/]

题意： Given the root of a binary tree, return the preorder traversal of its nodes' values.


#### 简洁回答

本题是经典的**二叉树前序遍历**问题。前序遍历的顺序是：

> **根节点 → 左子树 → 右子树**

使用递归可以轻松实现。

---

#### 详细回答

前序遍历的核心在于访问顺序。我们可以使用递归来实现这一逻辑：

1. 首先访问当前节点（根）；
2. 然后递归访问左子树；
3. 最后递归访问右子树。

该方法使用一个列表 `res` 来记录遍历顺序，在递归函数中不断追加节点值。

---



```python
def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        res = []
        def preorderHelper(cur_node):
            if cur_node == None:
                return
            
            res.append(cur_node.val)
            preorderHelper(cur_node.left)
            preorderHelper(cur_node.right)
            
        preorderHelper(root)
        return res
```
