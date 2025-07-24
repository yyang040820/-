## 113. Path Sum II

题目链接:[https://leetcode.com/problems/path-sum-ii/description/]

题意： Given the root of a binary tree and an integer targetSum, return all root-to-leaf paths where the sum of the node values in the path equals targetSum. Each path should be returned as a list of the node values, not node references.

A root-to-leaf path is a path starting from the root and ending at any leaf node. A leaf is a node with no children.


#### 简洁回答

这是一个典型的 **DFS + 回溯（Backtracking）** 问题。我们在深度优先遍历的同时维护一个路径列表，当回溯（即从子节点返回父节点）时要**撤销添加的节点**，以确保路径正确。

---

#### 详细解析

- 使用 DFS 遍历所有可能的从根到叶子的路径；
- 使用一个临时列表 `temp` 来记录当前路径；
- 每次递归减去当前节点值；
- 如果当前节点是叶子节点且剩余目标值等于当前节点值，则说明找到了一条合法路径；
- 回溯时记得将当前节点值从路径中移除（`temp.pop()`），避免影响其他路径。

---


```python
def pathSum(self, root: Optional[TreeNode], targetSum: int) -> List[List[int]]:
    res = []
    if root is None:
        return res

    def pathSumHelper(node, target, temp):
        if node is None:
            return

        temp.append(node.val)

        if node.left is None and node.right is None:
            if target == node.val:
                res.append(list(temp))
        else:
            pathSumHelper(node.left, target - node.val, temp)
            pathSumHelper(node.right, target - node.val, temp)

        temp.pop()  # backtrack

    pathSumHelper(root, targetSum, [])
    return res
```
