## 142.环形链表II

题目链接:[https://leetcode.com/problems/linked-list-cycle-ii/description/]

题意： 给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

为了表示给定链表中的环，使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。

说明：不允许修改给定的链表。

Example 1:\
![这是图片](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)
\
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.

Example 2:\
![这是图片](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

Input: head = [1,2], pos = 0
Output: tail connects to node index 0
Explanation: There is a cycle in the linked list, where tail connects to the first node.

Example 3:\
![这是图片](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png) 
\
Input: head = [1], pos = -1
Output: no cycle
Explanation: There is no cycle in the linked list.


Constraints:

The number of the nodes in the list is in the range [0, 104].
-105 <= Node.val <= 105
pos is -1 or a valid index in the linked-list.

#### 简洁回答
- **环检测：** 快慢指针相遇判定是否成环  
- **起点定位：** 利用数学推导起点到环的起始点距离等于快满指针相遇点到环起始点的较远距离，重置快指针至头部，双指针同步前行  
- **最终相遇：** 指向环的入口节点
- 
#### 详细回答
判断链表环起点可类比“快慢跑者追击”问题：若在环形跑道上，跑得快的选手追上跑得慢的选手，说明快者已多跑一圈。基于此，可分两步完成链表环检测与起点定位：

1. **检测环的存在**  
   - 使用快慢指针：快指针每次前进两步，慢指针每次前进一步。  
   - 若快指针遇到 `null`，则链表无环；若两指针相遇，则证明存在环。

2. **定位环的起点**  
   - 设从链表头到环起点的距离为 `x`，环起点到第一次相遇点的距离分为近段 `a` 和远段 `b`（环长 = `a + b`）。  
   - 慢指针走过距离 `x + a`；快指针走过 `x + 2a + b`。由于快者正好走了慢者两倍距离，可得 `2(x + a) = x + 2a + b`，解得 `x = b`。  
   - 因此，将快指针移回链表头，慢指针留在相遇点，双指针同步每次一步，二者相遇处即为环的起点。

---


```python
def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
    fast = head
    slow = head

    while fast != None and fast.next != None:
        slow = slow.next
        fast = fast.next.next
        if fast == slow:
            break
    
    if fast == None or fast.next == None:
        return None

    slow = head
    
    while fast != slow:
        fast = fast.next
        slow = slow.next
    
    return fast
```
