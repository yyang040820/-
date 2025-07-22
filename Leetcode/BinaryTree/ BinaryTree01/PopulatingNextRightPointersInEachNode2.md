## 117. Populating Next Right Pointers in Each Node II


题目链接:[https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/]


题意：Given a binary tree

struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.

#### 简洁回答

使用广度优先搜索（BFS）逐层遍历，通过一个临时指针连接每层的节点。

---

#### 详细回答

1. 利用队列进行层序遍历（BFS），确保节点按层顺序访问；
2. 对每一层的节点：
   - 用变量 `cur` 记录当前层中已连接的节点；
   - 遍历该层所有节点，依次设置 `cur.next` 指向下一个节点；
   - 第一节点单独赋值给 `cur`，后续节点用 `cur.next` 连接，并更新 `cur`；
3. 遍历完该层后，`cur.next` 自动为 `NULL`（或保持原有的 `NULL`）；
4. 重复上述步骤，直到遍历完所有层；
5. 返回修改后的根节点。

---

```python
def connect(self, root: 'Node') -> 'Node':
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
