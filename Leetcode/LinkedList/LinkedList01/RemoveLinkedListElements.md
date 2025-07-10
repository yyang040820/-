## 203.移除链表元素
题目链接
题意：删除链表中等于给定值 val 的所有节点。

示例 1： 输入：head = [1,2,6,3,4,5,6], val = 6 输出：[1,2,3,4,5]

示例 2： 输入：head = [], val = 1 输出：[]

示例 3： 输入：head = [7,7,7,7], val = 7 输出：[]
#### 简洁回答
引入哑结点后，无需对头节点和中间节点分开处理，所有删除操作都能使用相同的逻辑，从而简化代码实现。

#### 详细回答
在链表中删除元素时，只需将待删节点的前驱节点的 `next` 指针指向待删节点的后继节点即可。唯一的棘手情况是删除头节点，为此我们可以引入一个**哑结点**（Dummy）作为链表的虚拟起点，这样所有删除操作都能统一处理。

```python
def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        dummy = ListNode()
        dummy.next = head
        cur = head
        prev = dummy

        while cur:
            if cur.val == val:
                prev.next = cur.next
                cur = prev.next
            else:
                prev = cur
                cur = cur.next
        
        return dummy.next
```
