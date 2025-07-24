## 106. Construct Binary Tree from Inorder and Postorder Traversal

题目链接:[https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/description/]

题意： Given two integer arrays inorder and postorder where inorder is the inorder traversal of a binary tree and postorder is the postorder traversal of the same tree, construct and return the binary tree.

#### 简洁回答

这是一个典型的“已知中序 + 后序”重建二叉树问题。  
后序遍历的最后一个元素是当前子树的根节点，  
在中序遍历中找到该根节点的位置后，可以确定左右子树范围，然后递归构建。

---

#### 详细解析

构造流程如下：

1. 后序遍历的最后一个元素是当前子树的根节点；
2. 在中序遍历数组中找到该值的位置 `pivot`；
3. 中序数组中，`[in_start, pivot - 1]` 为左子树；
4. `[pivot + 1, in_end]` 为右子树；
5. 利用左右子树长度在后序数组中确定左右子树的区间；
6. 递归构建左右子树。

---

#### 注意事项

与“前序 + 中序”构建方式的最大区别是：
- **前序遍历从前往后**处理根节点；
- **后序遍历从后往前**处理根节点（即最后一个是当前子树根节点）。

---


```python
def buildTree(self, inorder: List[int], postorder: List[int]) -> Optional[TreeNode]:
    def buildTreeHelper(in_start,in_end,post_start,post_end):
        if in_start > in_end:
            return None

        pivot_value = postorder[post_end]
        cur_node = TreeNode(val = pivot_value)
        pivot = in_start
        for i in range(in_start,in_end+1):
            if inorder[i] == pivot_value:
                pivot = i
                break
        
        left_length = pivot - in_start
        right_length = in_end - pivot

        cur_node.left = buildTreeHelper(in_start,pivot - 1,post_start,post_end - right_length-1)
        cur_node.right = buildTreeHelper(pivot + 1,in_end,post_end - right_length,post_end - 1)

        return cur_node
    
    return buildTreeHelper(0,len(inorder)-1,0,len(postorder)-1)
```
