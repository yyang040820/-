## 94. Binary Tree Inorder Traversal

题目链接:[https://leetcode.com/problems/binary-tree-inorder-traversal/]

题意： Given the root of a binary tree, return the inorder traversal of its nodes' values.


#### 简洁回答

本题是经典的**二叉树中序遍历**问题。中序遍历的顺序是：

> **左子树 → 根节点 → 右子树**

可以使用递归方式简单实现。

---

#### 详细回答

中序遍历的核心是按如下顺序访问每个节点：

1. 先递归访问左子树；
2. 然后访问当前节点（根）；
3. 最后递归访问右子树。

这种遍历方式在二叉搜索树（BST）中尤为重要，因为它会按**从小到大**的顺序访问节点值。

我们使用递归函数辅助完成遍历，并将结果添加到列表 `res` 中。

---



```python
def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
    res = []

    def inorderHelper(cur):
        if cur == None:
            return
        
        inorderHelper(cur.left)
        res.append(cur.val)
        inorderHelper(cur.right)
    
    inorderHelper(root)

    return res
```
