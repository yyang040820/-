## 19. 删除链表的倒数第N个节点(需重点复习）

题目链接:[https://leetcode.com/problems/remove-nth-node-from-end-of-list/]

给你一个链表，删除链表的倒数第 n 个结点，并且返回链表的头结点。

Constraints:

The number of nodes in the list is sz.
1 <= sz <= 30
0 <= Node.val <= 100
1 <= n <= sz

进阶：你能尝试使用一趟扫描实现吗？

![例子1](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

输入：head = [1,2,3,4,5], n = 2 输出：[1,2,3,5]

示例 2：

输入：head = [1], n = 1 输出：[]

示例 3：

输入：head = [1,2], n = 1 输出：[1]

#### 简洁回答
- **暴力解法：** 两次遍历——一次求长度，一次删除指定位置  
- **优化解法：** 双指针一前一后保持 $n$ 步距离，快指针到尾即慢指针定位待删节点  
- **要点：** 始终保留待删节点的前驱，确保链表结构完整 

#### 详细回答

##### 暴力解法  
先遍历一次链表计算长度 $m$，再将第 $n$ 个节点从后向前转换为从前向后的第 $m - n + 1$ 位。第二次遍历至该位置，直接删除对应节点。

##### 优化解法  
利用双指针技巧：设置“快指针”比“慢指针”始终超前 $n$ 步。快指针到达链表末尾时，慢指针正好指向待删除节点。  
> **Tip:** 记录并维护待删除节点的前驱指针，否则删除时会丢失链表链接。

```python
//遍历两次
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

```python
//遍历1次
def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
      dummy = ListNode()
      dummy.next = head
      fast = dummy
      slow = dummy
      prev = None

      for i in range(n):
          fast = fast.next

      while fast != None and slow != None:
          fast = fast.next
          prev = slow
          slow = slow.next
      
      temp = slow.next
      prev.next = temp

      return dummy.next
```
