---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/225-implement-stack-using-queues/","tags":["Leetcode/Easy","Leetcode/代码随想录"],"noteIcon":"1"}
---


## 题目信息

- 链接: [implement-stack-using-queues](https://leetcode.cn/problems/implement-stack-using-queues/)
- Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (`push`, `top`, `pop`, and `empty`).

	Implement the `MyStack` class:
	
	-   `void push(int x)` Pushes element x to the top of the stack.
	-   `int pop()` Removes the element on the top of the stack and returns it.
	-   `int top()` Returns the element on the top of the stack.
	-   `boolean empty()` Returns `true` if the stack is empty, `false` otherwise.
	
	**Notes:**
	
	-   You must use **only** standard operations of a queue, which means that only `push to back`, `peek/pop from front`, `size` and `is empty` operations are valid.
	-   Depending on your language, the queue may not be supported natively. You may simulate a queue using a list or deque (double-ended queue) as long as you use only a queue's standard operations.
	
	**Example 1:**
	
	```
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
	
	```
	
	**Constraints:**
	-   `1 <= x <= 9`
	-   At most `100` calls will be made to `push`, `pop`, `top`, and `empty`.
	-   All the calls to `pop` and `top` are valid.
	
	**Follow-up:** Can you implement the stack using only one queue?

- 描述:
	- 请你仅使用两个队列实现一个后入先出（LIFO）的栈，并支持普通栈的全部四种操作（push、top、pop 和 empty）。
	- 实现 MyStack 类：
	- void push(int x) 将元素 x 压入栈顶。
	  int pop() 移除并返回栈顶元素。
	  int top() 返回栈顶元素。
	  boolean empty() 如果栈是空的，返回 true ；否则，返回 false 。

## 解题思路

- 其实只需要一个queue即可，由于queue先进先出，所以不管几个queue都不会改变顺序，所以和 [[1 P(Projects)/SDE Interview Prep/Algorithms/Leetcode/232 Implement Queue using Stacks\|232 用栈实现队列]] 有区别。
- 这里的思路是**把除了队尾的元素都暂时取出，然后再放回去**
- 两个队列可以把暂时取出的元素放入另一个队列，如果只使用一个队列，就直接取出元素放入队列末尾

## 代码

```python
  from collections import deque
  class MyStack:
  
	  def __init__(self):
		  self.q = deque()
  
	  def push(self, x: int) -> None:
		  self.q.append(x)
  
	  def pop(self) -> int:
		  s = len(self.q)
		  for i in range(s-1):
			  self.q.append(self.q.popleft())
		  return self.q.popleft()
  
	  def top(self) -> int:
		  s = len(self.q)
		  for i in range(s-1):
			  self.q.append(self.q.popleft())
		  re = self.q.popleft()
		  self.q.append(re)
		  return re
  
	  def empty(self) -> bool:
		  if len(self.q) == 0:
			  return True
		  else:
			  return False
```