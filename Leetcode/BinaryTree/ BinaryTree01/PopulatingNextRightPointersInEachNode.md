## 116. Populating Next Right Pointers in Each Node
题目链接:[https://leetcode.com/problems/populating-next-right-pointers-in-each-node/description/]


题意：You are given a perfect binary tree where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.

#### 简洁回答

使用广度优先搜索（BFS）逐层遍历节点，连接每层节点的 `next` 指针。

---

#### 详细回答

本质仍是层序遍历：

- 维护一个队列逐层访问节点；
- 遍历每层时，用变量 `cur` 记录当前已连接的节点；
- 对当前层的第一个节点，直接赋值 `cur`；
- 其余节点则通过 `cur.next` 指向当前节点，并更新 `cur`；
- 将子节点依次加入队列，供下一层遍历；
- 最终返回更新后的根节点。

---



```python
    def connect(self, root: 'Optional[Node]') -> 'Optional[Node]':
        if root == None:
            return root

        queue = deque([])
        queue.appendleft(root)
        
        while queue:
            cur_length = len(queue)
            cur = None
            for i in range(cur_length):
                pop_node = queue.pop()
                if i == 0:
                    cur = pop_node
                else:
                    cur.next = pop_node
                    cur = cur.next
                if pop_node.left:
                    queue.appendleft(pop_node.left)
                if pop_node.right:
                    queue.appendleft(pop_node.right)
        
        return root

```
