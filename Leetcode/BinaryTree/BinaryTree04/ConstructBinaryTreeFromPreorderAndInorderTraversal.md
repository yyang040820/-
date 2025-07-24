## 105. Construct Binary Tree from Preorder and Inorder Traversal

题目链接:[https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/]

题意： Given two integer arrays preorder and inorder where preorder is the preorder traversal of a binary tree and inorder is the inorder traversal of the same tree, construct and return the binary tree.


#### 简洁回答

利用前序遍历的根节点顺序和中序遍历的左右子树结构，可以递归地构建整棵树。

---

#### 详细解析

构建步骤如下：

1. **前序遍历的第一个元素**为当前子树的根节点；
2. 在 **中序遍历数组**中找到该根节点的位置（称为 `pivot`）；
3. 中序数组中，`[inorder_start, pivot)` 是**左子树**的中序遍历；
4. 中序数组中，`(pivot, inorder_end]` 是**右子树**的中序遍历；
5. 利用子树长度在前序数组中确定左右子树对应的区间；
6. 递归构建左右子树。

---

```python
def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
    def buildTreeHelper(preorder_start,preorder_end,inorder_start,inorder_end):
        if inorder_start > inorder_end:
            return None
        
        pivot_value = preorder[preorder_start]
        pivot_index = inorder_start
        cur_node = TreeNode(val = pivot_value)

        for i in range(inorder_start,inorder_end+1):
            if inorder[i] == pivot_value:
                pivot_index = i
                break
        
        left_child_length = pivot_index - inorder_start
        right_child_length = inorder_end - pivot_index

        cur_node.left = buildTreeHelper(preorder_start+1,preorder_start+left_child_length,inorder_start,pivot_index-1)
        cur_node.right = buildTreeHelper(preorder_start+left_child_length+1,preorder_end,pivot_index+1,inorder_end)

        return cur_node
    
    return buildTreeHelper(0,len(preorder)-1,0,len(inorder)-1)
```
