## 222. Count Complete Tree Nodes

题目链接:[https://leetcode.com/problems/count-complete-tree-nodes/]

题意： Given the root of a complete binary tree, return the number of the nodes in the tree.

According to Wikipedia, every level, except possibly the last, is completely filled in a complete binary tree, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.

Design an algorithm that runs in less than O(n) time complexity.




#### 简洁回答

本题要求统计一棵二叉树的节点总数。最直接的做法是使用递归遍历整棵树，对每个节点进行计数。

---

#### 详细回答

第一轮刷题中，我们使用了一个非常直接的递归解法：

- 对于每个非空节点，计数加一；
- 然后递归地对左右子树分别处理；
- 最终统计所有节点的数量。

该方法虽然简单有效，但**时间复杂度为 O(N)**，其中 N 是树中节点总数。

---

#### 优化方向（预告）

如果我们进一步利用**完全二叉树（Complete Binary Tree）**的特性，可以将时间复杂度优化为 **O(logN × logN)**。该优化思路涉及判断子树是否为满二叉树，从而避免对所有节点的逐一遍历。

由于该优化稍复杂，建议在后续刷题中深入理解并实现。

---

```python
def countNodes(self, root: Optional[TreeNode]) -> int:
      res = 0

      def countNodesHelper(root):
          nonlocal res
          if root == None:
              return
          
          res += 1
          countNodesHelper(root.left)
          countNodesHelper(root.right)
      
      countNodesHelper(root)
      return res

```
