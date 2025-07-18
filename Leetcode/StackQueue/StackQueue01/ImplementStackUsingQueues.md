## 225.Implement Stack using Queues

题目链接:[https://leetcode.com/problems/implement-stack-using-queues/description/]

题意： 
Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (push, top, pop, and empty).

Implement the MyStack class:

void push(int x) Pushes element x to the top of the stack.
int pop() Removes the element on the top of the stack and returns it.
int top() Returns the element on the top of the stack.
boolean empty() Returns true if the stack is empty, false otherwise.
Notes:

You must use only standard operations of a queue, which means that only push to back, peek/pop from front, size and is empty operations are valid.
Depending on your language, the queue may not be supported natively. You may simulate a queue using a list or deque (double-ended queue) as long as you use only a queue's standard operations.
 

Example 1:

Input
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]
Output
[null, null, null, 2, 2, false]

Explanation
MyStack myStack = new MyStack();
myStack.push(1);
myStack.push(2);
myStack.top(); // return 2
myStack.pop(); // return 2
myStack.empty(); // return False
 

Constraints:

1 <= x <= 9
At most 100 calls will be made to push, pop, top, and empty.
All the calls to pop and top are valid.
 

Follow-up: Can you implement the stack using only one queue?

#### 简洁回答
只用一个队列（queue）也能实现栈（stack）的功能。在每次 `push` 时，将当前元素加入队列尾部，然后将之前的所有元素依次出队再重新入队，从而让新元素始终处于队首，实现后进先出（LIFO）的效果。

#### 详细回答
乍一看，实现栈的功能似乎需要两个队列来互相倒腾元素。但实际上，我们只需要一个队列就能模拟栈的行为。

核心思路如下：
- **Push 操作**：先将新元素加入队列末尾，再将原队列中的元素依次弹出再加入队尾，从而让新元素转到队首（模拟栈顶）。
- **Pop 操作**：由于新元素已经在队首，直接弹出队尾即可。
- **Top 操作**：访问队尾元素，即当前栈顶元素。
- **Empty 操作**：检查队列是否为空即可。

通过这种方式，我们用队列实现了栈的“后进先出”行为，代码简洁、效率也较高。

---


```python
class MyStack:
    def __init__(self):
        self.queue = deque([])
        self.size = 0

    def push(self, x: int) -> None:
        self.queue.appendleft(x)
        self.cur = x
        for _ in range(self.size):
            self.queue.appendleft(self.queue.pop())
        self.size += 1
        print(self.queue)
        

    def pop(self) -> int:
        cur = self.queue.pop() 
        self.size -= 1
        return cur
        

    def top(self) -> int:
        if len(self.queue) == 0:
            return None
        else:
            return self.queue[-1]
        

    def empty(self) -> bool:
        return len(self.queue) == 0
```
