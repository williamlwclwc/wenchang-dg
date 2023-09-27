---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/232-implement-queue-using-stacks/","tags":["Leetcode/Easy","Leetcode/代码随想录"],"noteIcon":"1"}
---

## 题目信息

- 链接: [implement-queue-using-stacks](https://leetcode.cn/problems/implement-queue-using-stacks/)
- Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (`push`, `peek`, `pop`, and `empty`).
  
  Implement the `MyQueue` class:

	-   `void push(int x)` Pushes element x to the back of the queue.
	-   `int pop()` Removes the element from the front of the queue and returns it.
	-   `int peek()` Returns the element at the front of the queue.
	-   `boolean empty()` Returns `true` if the queue is empty, `false` otherwise.
	
	**Notes:**
	
	-   You must use **only** standard operations of a stack, which means only `push to top`, `peek/pop from top`, `size`, and `is empty` operations are valid.
	-   Depending on your language, the stack may not be supported natively. You may simulate a stack using a list or deque (double-ended queue) as long as you use only a stack's standard operations.
	
	**Example 1:**
	
	```
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
	
	```
	
	**Constraints:**
	
	-   `1 <= x <= 9`
	-   At most `100` calls will be made to `push`, `pop`, `peek`, and `empty`.
	-   All the calls to `pop` and `peek` are valid.
	
	**Follow-up:** Can you implement the queue such that each operation is **[amortized](https://en.wikipedia.org/wiki/Amortized_analysis)** `O(1)` time complexity? In other words, performing `n` operations will take overall `O(n)` time even if one of those operations may take longer.

- 描述:
	- 请你仅使用两个栈实现先入先出队列。队列应当支持一般队列支持的所有操作（push、pop、peek、empty）：
	- 实现 MyQueue 类：
	- void push(int x) 将元素 x 推到队列的末尾
	  int pop() 从队列的开头移除并返回元素
	  int peek() 返回队列开头的元素
	  boolean empty() 如果队列为空，返回 true ；否则，返回 false
	  说明：
	- 你 只能 使用标准的栈操作 —— 也就是只有 push to top, peek/pop from top, size, 和 is empty 操作是合法的。
	  你所使用的语言也许不支持栈。你可以使用 list 或者 deque（双端队列）来模拟一个栈，只要是标准的栈操作即可。

## 解题思路

- 思路在于用**一个stack1来入队，另一个stack2出队**
- 出队时，要让先入队的元素先出，所以要让stack2的顺序和stack1相反。
	- 具体来说就是将stack1元素依次出栈，然后再入栈stack2，这样stack2栈顶就是stack1的栈底，这样stack2出栈的就是队首元素
- 另外就是*什么时候*将stack1元素倒入stack2？
	- stack2是用来获取队首元素的，所以当pop/peek而stack2为空，stack1不为空时，就将stack1的元素倒入stack2即可

## 代码

```python
class MyQueue:

    def __init__(self):
        self.stack1 = []
        self.stack2 = []


    def push(self, x: int) -> None:
        self.stack1.append(x)

	# do not need to check empty 
	# since all pop and peek are valid
    def pop(self) -> int:
        self.trans_s1_to_s2()
        return self.stack2.pop()


    def peek(self) -> int:
        self.trans_s1_to_s2()
        return self.stack2[-1]


    def empty(self) -> bool:
        if len(self.stack1) == 0 and len(self.stack2) == 0:
            return True
        else:
            return False

	# if s2 is empty, put all ele in s1 to s2
    def trans_s1_to_s2(self) -> None:
        if len(self.stack2) == 0:
            for _ in range(len(self.stack1)):
                self.stack2.append(self.stack1.pop())



# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()
```