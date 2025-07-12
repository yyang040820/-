## 24. 两两交换链表中的节点 
题目链接:[https://leetcode.com/problems/swap-nodes-in-pairs/description/]

给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

#### 简洁回答

- 识别并维护四个关键节点：前驱、节点1、节点2、后继
- 通过奇偶步交替：奇数步移动指针，偶数步执行断开与重连
- 在偶数步中备份后继节点，按顺序重连实现节点交换
- 保证交换过程中与相邻节点的链接始终完整```

#### 详细回答
在交换链表中的两个节点时，实际上涉及四个节点：待交换的节点（记为节点1和节点2），节点1 的前驱节点，以及节点2的后继节点。仅仅互换节点1和节点2本身，会导致它们与前驱和后继节点的链接丢失，类似于反转链表却只处理了局部。

我的解决方案利用一个计数器 `count` 来交替执行不同操作：  
1. **奇数步**：不做实际交换，仅将三个指针 —— `prev_prev`（节点1的前驱）、`prev`（节点1）、`cur`（节点2） —— 同时向后移动一位。  
2. **偶数步**：先保存节点2 的后继 `next_cur`，然后依次重连：  
   - `prev_prev.next` 指向 节点2  
   - `cur.next` 指向 节点1  
   - `prev.next` 指向 `next_cur`  
   重连后，将 `prev_prev` 更新为原节点2，`cur` 更新为原节点2 的后继，`prev`（节点1）保持不变，以便下一轮继续移动或交换。

---



```python
def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head == None:
            return head
        
        dummy = ListNode()
        dummy.next = head
        prev_prev = dummy
        prev = prev_prev.next
        cur = prev.next
        count = 0

        while cur:
            if count % 2 == 0:
                temp = cur.next
                prev_prev.next = cur
                cur.next = prev
                prev.next = temp
                
                prev_prev = cur
                cur = temp

            else:
                prev_prev = prev
                prev = cur
                cur = cur.next
                
            count += 1
        
        return dummy.next
```
