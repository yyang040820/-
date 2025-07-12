## 160 链表相交

题目链接:[https://leetcode.com/problems/intersection-of-two-linked-lists/description/]
给你两个单链表的头节点 headA 和 headB ，请你找出并返回两个单链表相交的起始节点。如果两个链表没有交点，返回 null 。

例子
![例子](https://assets.leetcode.com/uploads/2021/03/05/160_statement.png)

#### 简洁回答
- 计算两链表长度差  
- 让长链表先走差值步  
- 同步移动并比较节点  
- 相同即为交点，否则无交集

#### 详细回答
先分别遍历两个链表，计算长度 `m` 和 `n`。令较长链表的指针先行走 `|m - n|` 步，使两条链表剩余长度相等；然后同时移动两个指针，每次比较它们指向的节点：  
- 若节点相同，则找到交点，直接返回该节点；  
- 若遍历至链表末尾仍无相同节点，则返回 `null`，表示链表不相交。

> **备注：** 虽然存在通过“交换指针起点”实现更简洁的方案，但面试中解释成本较高，且易混淆，权衡之下不如本方法直观。

---

```python
def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
    dummy = ListNode()
    dummy.next = head
    cur = dummy
    
    count = 0
    while cur != None:
        cur = cur.next
        count = count + 1
    
    target = count - n

    count = 0
    cur = dummy
    prev = None

    while count < target:
        prev = cur
        cur = cur.next
        count = count + 1
    
    temp = cur.next
    prev.next = temp

    return dummy.next
```
