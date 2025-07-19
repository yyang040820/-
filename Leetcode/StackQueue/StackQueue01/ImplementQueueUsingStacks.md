## 232 Implement Queue using Stacks

题目链接:[https://leetcode.com/problems/implement-queue-using-stacks/]

题意： 
Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).

Implement the MyQueue class:

void push(int x) Pushes element x to the back of the queue.
int pop() Removes the element from the front of the queue and returns it.
int peek() Returns the element at the front of the queue.
boolean empty() Returns true if the queue is empty, false otherwise.
Notes:

You must use only standard operations of a stack, which means only push to top, peek/pop from top, size, and is empty operations are valid.
Depending on your language, the stack may not be supported natively. You may simulate a stack using a list or deque (double-ended queue) as long as you use only a stack's standard operations.
 

Example 1:

Input
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
Output
[null, null, null, 1, 1, false]

Explanation
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false
 

Constraints:

1 <= x <= 9
At most 100 calls will be made to push, pop, peek, and empty.
All the calls to pop and peek are valid.
 

Follow-up: Can you implement the queue such that each operation is amortized O(1) time complexity? In other words, performing n operations will take overall O(n) time even if one of those operations may take longer.

#### 简洁回答
使用两个栈（stack）可以实现一个队列（queue），并且所有操作的**摊还时间复杂度（Amortized Time Complexity）为 O(1)**。一个栈用于入队（push），另一个用于出队（pop）。只有在出队栈为空时，才将入队栈的所有元素倒入，这样避免了每次出队都进行搬运。

#### 详细回答
为了实现一个高效的队列结构，并保证 `push`、`pop`、`peek` 和 `empty` 操作的摊还时间复杂度为 O(1)，我们可以使用两个栈：

- `stack_1`: 负责所有的 `push` 操作；
- `stack_2`: 负责所有的 `pop` 和 `peek` 操作。

核心思想如下：
- `push(x)`：将元素直接压入 `stack_1`，时间复杂度为 O(1)。
- `pop()` / `peek()`：只有当 `stack_2` 为空时，才把 `stack_1` 中的所有元素倒序压入 `stack_2`，这样原来先进的元素会在顶部，实现队列的先进先出（FIFO）逻辑。
- `empty()`


```python
class MyQueue:
    def __init__(self):
        self.stack_1 = []
        self.stack_2 = []
        self.size = 0
        

    def push(self, x: int) -> None:
        self.stack_1.append(x)
        self.size += 1
        

    def pop(self) -> int:
        if len(self.stack_2) == 0:
            while len(self.stack_1) > 0:
                temp = self.stack_1.pop()
                self.stack_2.append(temp)
        self.size -= 1
        return self.stack_2.pop()
        
        

    def peek(self) -> int:
        if len(self.stack_2) == 0:
            while len(self.stack_1) > 0:
                temp = self.stack_1.pop()
                self.stack_2.append(temp)
        return self.stack_2[-1]
        

    def empty(self) -> bool:
        return len(self.stack_1) == 0 and len(self.stack_2) == 0
```
