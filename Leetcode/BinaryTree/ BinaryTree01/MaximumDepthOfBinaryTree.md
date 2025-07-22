## 104. Maximum Depth of Binary Tree


题目链接:[https://leetcode.com/problems/maximum-depth-of-binary-tree/description/]


题意：Given the root of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.



#### 简洁回答

使用深度优先搜索（DFS）递归计算左右子树深度，取最大值加一。

---

#### 详细回答

思路：

- 递归遍历二叉树；
- 当节点为空时，返回深度 0；
- 递归计算左、右子树深度，取较大者加1作为当前节点的深度；
- 递归返回最大深度。

也可以用BFS数层数。
---



```python
//DFS
def maxDepth(self, root: Optional[TreeNode]) -> int:
      def depthCounter(root):
          if root == None:
              return 0
          
          left_count = depthCounter(root.left)
          right_count = depthCounter(root.right)

          return max(left_count,right_count) + 1
      
      return depthCounter(root)

```



