## 257. Binary Tree Paths

题目链接:[https://leetcode.com/problems/binary-tree-paths/description/]

题意：Given the root of a binary tree, return all root-to-leaf paths in any order.

A leaf is a node with no children.

Constraints:

The number of nodes in the tree is in the range [1, 100].
-100 <= Node.val <= 100


#### 简洁回答

本题要求返回所有从根节点到叶子节点的路径。我们可以通过递归遍历整棵树，在遍历过程中记录路径，当到达叶子节点时将路径加入结果列表。

---

#### 详细回答

要返回一棵二叉树的所有根到叶子的路径，核心思路是：

1. 遍历整棵树（深度优先搜索）；
2. 使用一个临时路径变量 `temp` 记录当前路径；
3. **当到达叶子节点时**，将路径加入结果列表；
4. **遇到空节点时**，直接返回，避免路径被重复添加。

一个容易犯的错误是在遇到 `None` 时就将路径加入结果列表，这样会导致重复或错误的路径记录。正确做法是在遍历到**叶子节点（左右孩子都为空）**时才添加路径。

---

#### 时间复杂度分析

- **遍历所有节点的时间复杂度为 O(N)**，其中 N 是节点总数；
- 每条路径的最大长度为树的高度，平衡树中为 O(logN)；
- 假设树有 N/2 个叶子节点，则路径总长度为 O((N/2) × logN) = O(NlogN)；
- 因此总时间复杂度为：**O(N + NlogN) = O(NlogN)**；

当然，如果使用迭代法，还可以将时间复杂度优化到 **O(N)**，这部分可以在后续学习中继续深入。

---

```python
def binaryTreePaths(self, root: Optional[TreeNode]) -> List[str]:
      res = []

      def traversalHelper(root,temp):
          if root == None:
              return

          temp = temp + '->' + str(root.val)
          if root.left == None and root.right == None:
              res.append(temp[2:])
          
          traversalHelper(root.left,temp)
          traversalHelper(root.right,temp)

      traversalHelper(root,'')
      return res
```
