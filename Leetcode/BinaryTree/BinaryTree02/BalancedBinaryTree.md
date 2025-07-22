## 101 Balanced Binary Tree

题目链接:[https://leetcode.com/problems/balanced-binary-tree/]

题意： Given a binary tree, determine if it is height-balanced (A height-balanced binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one).


#### 简洁回答

判断一棵二叉树是否平衡，可以通过递归检查每个节点的左右子树是否也平衡，并且它们的高度差是否不超过 1。

---

#### 详细回答

要判断一棵二叉树是否平衡，我们可以从以下两个角度出发：

1. **左右子树是否平衡**：如果左子树或右子树本身不平衡，则整棵树也不平衡；
2. **左右子树高度差**：如果左右子树的高度差超过 1，则该节点处不平衡，整棵树也不平衡。

因此，我们在递归判断的过程中，需要返回两个信息：

- 当前子树是否平衡；
- 当前子树的高度。

基本思路如下：

1. 如果当前节点是 `None`，说明是空树，平衡且高度为 0；
2. 否则，递归判断左右子树是否平衡，并计算它们的高度；
3. 如果任一子树不平衡，或高度差超过 1，则当前子树不平衡；
4. 否则，当前子树平衡，其高度为左右子树最大高度加 1。

---


```python
def isBalanced(self, root: Optional[TreeNode]) -> bool:

      def balanceHelper(root):
          if root == None:
              return True,0
          
          res_left,left_height = balanceHelper(root.left)
          res_right,right_height = balanceHelper(root.right)

          if res_left == False or res_right == False or abs(left_height-right_height) > 1:
              return False,None
          
          return True, max(left_height,right_height)+1
      
      res,count = balanceHelper(root)
      return res
```
