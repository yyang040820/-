## 206.反转链表

题目链接：[https://leetcode.com/problems/reverse-linked-list/]

题意：反转一个单链表。

示例: 输入: 1->2->3->4->5->NULL 输出: 5->4->3->2->1->NULL

#### 简洁回答
通过在反转前缓存后继节点，确保每次指针替换都不会丢失链表剩余部分，从而安全、完整地实现链表反转
#### 详细回答
本题的关键在于反转过程中对指针关系的妥善保存。在将当前节点的 `next` 指针指向前驱节点之前，必须先备份它原有的后继节点，否则链表其余部分将丢失。具体做法是在遍历时，对于每个节点同时维护两个指针：一个指向当前节点，另一个缓存它的前继节点；然后执行指针替换——先备份 `next`，再将当前节点的 `next` 指针指向前驱，逐步完成反转。

```python
def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None
        cur = head

        while cur:
            temp = cur.next
            cur.next = prev
            prev = cur
            cur = temp
        
        return prev
```
