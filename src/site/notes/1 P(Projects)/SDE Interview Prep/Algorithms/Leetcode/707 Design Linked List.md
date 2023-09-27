---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/707-design-linked-list/","tags":["Leetcode/Medium","Leetcode/代码随想录"],"noteIcon":"1"}
---

## 题目信息

- 链接: [design-linked-list](https://leetcode.cn/problems/design-linked-list/)
- 设计链表的实现。您可以选择使用单链表或双链表。单链表中的节点应该具有两个属性：val 和 next。val 是当前节点的值，next 是指向下一个节点的指针/引用。如果要使用双向链表，则还需要一个属性 prev 以指示链表中的上一个节点。假设链表中的所有节点都是 0-index 的。
	- 在链表类中实现这些功能：
	- get(index)：获取链表中第 index 个节点的值。如果索引无效，则返回-1。
	  addAtHead(val)：在链表的第一个元素之前添加一个值为 val 的节点。插入后，新节点将成为链表的第一个节点。
	  addAtTail(val)：将值为 val 的节点追加到链表的最后一个元素。
	  addAtIndex(index,val)：在链表中的第 index 个节点之前添加值为 val  的节点。如果 index 等于链表的长度，则该节点将附加到链表的末尾。如果 index 大于链表长度，则不会插入节点。如果index小于0，则在头部插入节点。
	  deleteAtIndex(index)：如果索引 index 有效，则删除链表中的第 index 个节点。
- Design your implementation of the linked list. You can choose to use a singly or doubly linked list.
  A node in a singly linked list should have two attributes: val and next. val is the value of the current node, and next is a pointer/reference to the next node.
  If you want to use the doubly linked list, you will need one more attribute prev to indicate the previous node in the linked list. Assume all nodes in the linked list are 0-indexed.
	- Implement the MyLinkedList class:
	- MyLinkedList() Initializes the MyLinkedList object.
	  int get(int index) Get the value of the indexth node in the linked list. If the index is invalid, return -1.
	  void addAtHead(int val) Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list.
	  void addAtTail(int val) Append a node of value val as the last element of the linked list.
	  void addAtIndex(int index, int val) Add a node of value val before the indexth node in the linked list. If index equals the length of the linked list, the node will be appended to the end of the linked list. If index is greater than the length, the node will not be inserted.
	  void deleteAtIndex(int index) Delete the indexth node in the linked list, if the index is valid.

## 解题思路

- 没有什么技巧，需要判断index是否合法
- 包含了 [[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Linked List\|Linked List]] 相关增删改查的基础操作
- 使用 [[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Linked List#Dummy Node 哑巴/虚拟节点\|dummy node]] 操作头节点稍微容易一些，不用也可以

## 代码

```python
  class ListNode:
	  def __init__(self, val=0, next=None):
		  self.val = val
		  self.next = next
  
  class MyLinkedList:
  
	  def __init__(self):
		  self.head = None
  
  
	  def get(self, index: int) -> int:
		  cur = 0
		  p = self.head
		  while p != None:
			  if cur == index:
				  return p.val
			  p = p.next
			  cur += 1
		  return -1
  
  
	  def addAtHead(self, val: int) -> None:
		  newHead = ListNode(val)
		  newHead.next = self.head
		  self.head = newHead
  
  
	  def addAtTail(self, val: int) -> None:
		  newTail = ListNode(val)
		  if self.head == None:
			  self.head = newTail
			  return
		  p = self.head
		  while p.next != None:
			  p = p.next
		  p.next = newTail
  
  
	  def addAtIndex(self, index: int, val: int) -> None:
		  if index <= 0:
			  self.addAtHead(val)
			  return
		  cur = 0
		  p = self.head
		  while p != None:
			  if cur + 1 == index:
				  newNode = ListNode(val)
				  newNode.next = p.next
				  p.next = newNode
				  return
			  p = p.next
			  cur += 1
  
  
	  def deleteAtIndex(self, index: int) -> None:
		  if index < 0:
			  return
		  cur = 0
		  p = self.head
		  if index == 0:
			  self.head = p.next
			  p.next = None
			  return
		  while p != None:
			  if cur + 1 == index and p.next != None:
				  p.next = p.next.next
				  return
			  p = p.next
			  cur += 1
  
  
  # Your MyLinkedList object will be instantiated and called as such:
  # obj = MyLinkedList()
  # param_1 = obj.get(index)
  # obj.addAtHead(val)
  # obj.addAtTail(val)
  # obj.addAtIndex(index,val)
  # obj.deleteAtIndex(index)
  ```