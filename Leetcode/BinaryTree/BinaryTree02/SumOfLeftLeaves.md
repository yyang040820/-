## 404. Sum of Left Leaves

题目链接:[https://leetcode.com/problems/sum-of-left-leaves/description/]

题意： Given the root of a binary tree, return the sum of all left leaves.

A leaf is a node with no children. A left leaf is a leaf that is the left child of another node.

Constraints:

The number of nodes in the tree is in the range [1, 1000].
-1000 <= Node.val <= 1000

#### 简洁回答

本题要求计算所有**左叶子节点**的和。我们可以通过递归遍历整棵树，在遍历过程中判断每个节点是否为左叶子节点，并进行累加。

---

#### 详细回答

要解决“左叶子之和”的问题，关键在于正确判断两个条件：

1. **左节点**：当前节点是其父节点的左孩子；
2. **叶子节点**：该节点没有左右子节点（`left == None` 且 `right == None`）。

为此，我们可以使用一个递归辅助函数，并引入一个标志位 `flag` 来标识当前节点是左子节点还是右子节点：

- `flag = 0` 表示当前节点是左子节点；
- `flag = 1` 表示当前节点是右子节点；
- 初始时传入 `flag = 0` 即可。

另外，在 Python 中，如果我们在嵌套函数中需要修改外层函数的变量（如 `res`），则需要使用 `nonlocal` 关键字。

---



```python
def sumOfLeftLeaves(self, root: Optional[TreeNode]) -> int:
        res = 0
        if root == None or (root.left == None and root.right == None):
            return res
            
        def leftLevesSum(root,flag):
            nonlocal res
            if root == None:
                return
            
            if root.left == None and root.right == None and flag == 0:
                res += root.val
            
            leftLevesSum(root.left,0)
            leftLevesSum(root.right,1)
        
        leftLevesSum(root,0)
        return res
```
