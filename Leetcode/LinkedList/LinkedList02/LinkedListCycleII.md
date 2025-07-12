## 142.环形链表II

题目链接:[https://leetcode.com/problems/linked-list-cycle-ii/description/]

题意： 给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

为了表示给定链表中的环，使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。

说明：不允许修改给定的链表。

Example 1:
![这是图片](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.
Example 2:
![这是图片](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

Input: head = [1,2], pos = 0
Output: tail connects to node index 0
Explanation: There is a cycle in the linked list, where tail connects to the first node.
Example 3:


Input: head = [1], pos = -1
Output: no cycle
Explanation: There is no cycle in the linked list.
![这是图片](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png) 

Constraints:

The number of the nodes in the list is in the range [0, 104].
-105 <= Node.val <= 105
pos is -1 or a valid index in the linked-list.

#### 简洁回答

#### 详细回答


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
