## 707.设计链表
题目链接: [https://leetcode.com/problems/design-linked-list/description/]
题意：

在链表类中实现这些功能：

get(index)：获取链表中第 index 个节点的值。如果索引无效，则返回-1。
addAtHead(val)：在链表的第一个元素之前添加一个值为 val 的节点。插入后，新节点将成为链表的第一个节点。
addAtTail(val)：将值为 val 的节点追加到链表的最后一个元素。
addAtIndex(index,val)：在链表中的第 index 个节点之前添加值为 val  的节点。如果 index 等于链表的长度，则该节点将附加到链表的末尾。如果 index 大于链表长度，则不会插入节点。如果index小于0，则在头部插入节点。
deleteAtIndex(index)：如果索引 index 有效，则删除链表中的第 index 个节点。

#### 简洁回答
该设计通过：  
- 专用 `Node` 类存储节点值与指针，  
- 单向链表使用哑头（Dummy Head）、双向链表同时引入哑头和哑尾（Dummy Tail）以统一处理边界插入/删除，  
- `self.size` 属性实现常量时间的索引合法性检查，  

从而让 `get(index)`、`addAtHead(val)`、`addAtTail(val)`、`addAtIndex(index,val)` 和 `deleteAtIndex(index)` 等操作无需特殊分支判断，逻辑一致且易于维护。  

#### 详细回答
- **节点类设计**  
  为链表创建专有的 `Node` 类存储节点值。在单向链表中使用一个哑头节点（Dummy Head）以简化插入和删除操作；在双向链表中则同时使用哑头和哑尾节点（Dummy Head & Dummy Tail）。

- **维护长度**  
  在初始化时引入 `self.size` 属性，用于跟踪链表当前长度。这样在所有以索引为依据的操作中，只需检查 `0 ≤ index < self.size`（或 `index == self.size` 允许插入尾部），即可判定索引有效性。

- **`get(index)`**  
  - 检验 `index` 是否在 `[0, self.size)` 范围内；  
  - 从哑头开始沿 `next` 指针遍历 `index+1` 步，返回目标节点的值。

- **`addAtHead(val)`**  
  - 新建节点，将其 `next` 指向原第一个节点（哑头的 `next`）；  
  - 更新哑头的 `next` 为新节点；  
  - `self.size += 1`。

- **`addAtTail(val)`**  
  - **单向链表**：遍历至尾节点（最后一个有效节点），将其 `next` 指向新节点；  
  - **双向链表**：直接将新节点插入哑尾之前；  
  - `self.size += 1`。

- **`addAtIndex(index, val)`**  
  - 若 `index` 超出 `(0, self.size]` 范围，则无效；  
  - 遍历至 `index` 前驱节点，将新节点插入前驱与后继之间；  
  - `self.size += 1`。（允许 `index == self.size` 作为尾插）

- **`deleteAtIndex(index)`**  
  - 仅当 `0 ≤ index < self.size` 时执行；  
  - 遍历至待删节点，用其前驱的 `next` 跳过当前节点指向后继；  
  - `self.size -= 1`。


```python
// 单向链表
class MyLinkedList:
    class LinkedNode:
        def __init__(self,val = 0,next = None):
            self.val = val
            self.next = None
            

    def __init__(self):
        self.size = 0
        self.head = self.LinkedNode()
        

    def get(self, index: int) -> int:
        if index >= self.size:
            return -1
        
        count = -1
        cur = self.head
        while count < index:
            cur = cur.next
            count = count + 1
        
        return cur.val

        
    def addAtHead(self, val: int) -> None:
        temp = self.LinkedNode(val)
        original_next = self.head.next

        self.head.next = temp
        temp.next = original_next

        self.size += 1

    def addAtTail(self, val: int) -> None:
        temp = self.LinkedNode(val)
        prev = self.head
        cur = self.head.next

        while cur:
            prev = cur
            cur = cur.next
        
        prev.next = temp  
        self.size += 1


    def addAtIndex(self, index: int, val: int) -> None:
        if index > self.size:
            return 
        
        count = -1
        cur = self.head
        prev = None
        while count < index:
            prev = cur
            cur = cur.next
            count = count + 1
        
        temp = self.LinkedNode(val)
        prev.next = temp
        temp.next = cur
        
        self.size += 1


    def deleteAtIndex(self, index: int) -> None:
        if index >= self.size:
            return 
        
        count = -1
        cur = self.head
        prev = None
        while count < index:
            prev = cur
            cur = cur.next
            count = count + 1
        
        original_next = cur.next
        prev.next = original_next

        self.size -= 1
```

```python
// 双向链表
class MyLinkedList:
    class LinkedNode:
        def __init__(self,val=0):
            self.val = val
            self.next = None
            self.prev = None

    def __init__(self):
        self.size = 0
        self.head = self.LinkedNode()
        self.tail = self.LinkedNode()
        self.head.next = self.tail
        self.tail.prev = self.head
        

    def get(self, index: int) -> int:
        if index >= self.size:
            return -1
        
        backward_index = self.size - index
        

        if backward_index <= index:
            count = 0
            cur = self.tail
            while count < backward_index:
                cur = cur.prev
                count = count + 1
        else:
            count = -1
            cur = self.head
            while count < index:
                cur = cur.next
                count = count + 1
        
        return cur.val

        
    def addAtHead(self, val: int) -> None:
        temp = self.LinkedNode(val)
        original_next = self.head.next

        self.head.next = temp
        temp.prev = self.head

        temp.next = original_next
        original_next.prev = temp

        self.size += 1

    def addAtTail(self, val: int) -> None:
        temp = self.LinkedNode(val)
        original_prev = self.tail.prev

        self.tail.prev = temp
        temp.next = self.tail

        original_prev.next = temp
        temp.prev = original_prev
        self.size += 1


    def addAtIndex(self, index: int, val: int) -> None:
        if index > self.size:
            return 
        
        backward_index = self.size - index
        if backward_index <= index:
            count = 0
            cur = self.tail
            while count < backward_index:
                cur = cur.prev
                count = count + 1
        else:
            count = -1
            cur = self.head
            while count < index:
                cur = cur.next
                count = count + 1
        
        temp = self.LinkedNode(val)
        original_prev = cur.prev
        original_prev.next = temp
        temp.prev = original_prev

        cur.prev = temp
        temp.next = cur
        self.size += 1


    def deleteAtIndex(self, index: int) -> None:
        if index >= self.size:
            return 
        
        backward_index = self.size - index
        if backward_index <= index:
            count = 0
            cur = self.tail
            while count < backward_index:
                cur = cur.prev
                count = count + 1
        else:
            count = -1
            cur = self.head
            while count < index:
                cur = cur.next
                count = count + 1
        
        original_next = cur.next
        original_prev = cur.prev
        original_prev.next = original_next
        original_next.prev = original_prev
        self.size -= 1
# Your MyLinkedList object will be instantiated and called as such:
# obj = MyLinkedList()
# param_1 = obj.get(index)
# obj.addAtHead(val)
# obj.addAtTail(val)
# obj.addAtIndex(index,val)
# obj.deleteAtIndex(index)
```
