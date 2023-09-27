---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/203-remove-linked-list-elements/","tags":["Leetcode/Easy","Leetcode/代码随想录"],"noteIcon":"1"}
---

## 题目信息

- 链接: [remove-linked-list-elements](https://leetcode.cn/problems/remove-linked-list-elements/)
- Given the `head` of a linked list and an integer `val`, remove all the nodes of the linked list that has `Node.val == val`, and return _the new head_.
  
  **Example 1:**
  
  ![](https://assets.leetcode.com/uploads/2021/03/06/removelinked-list.jpg)
  
  ```
  Input: head = [1,2,6,3,4,5,6], val = 6
  Output: [1,2,3,4,5]
  
  ```
  
  **Example 2:**
  
  ```
  Input: head = [], val = 1
  Output: []
  
  ```
  
  **Example 3:**
  
  ```
  Input: head = [7,7,7,7], val = 7
  Output: []
  
  ```
  
  **Constraints:**
	- The number of nodes in the list is in the range `[0, 10<sup>4</sup>]`.
	- `1 <= Node.val <= 50`
	- `0 <= val <= 50`

- 描述:
	- 给你一个链表的头节点 head 和一个整数 val ，请你删除链表中所有满足 Node.val == val 的节点，并返回新的头节点。

## 解题思路

- 遍历链表，找到值等于val的节点v的前一个节点，删除链表元素v [[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Linked List#删除节点\|删除节点]]
- 因为可能会删除头节点所以使用 [[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Linked List#Dummy Node 哑巴/虚拟节点\|dummy node]]
- 需要删除所有值等于val的节点，所以需要使用while循环持续删除节点
- 注意获取 `p.val` 时p是否可能为None

## 代码

```python
  # Definition for singly-linked list.
  # class ListNode:
  #     def __init__(self, val=0, next=None):
  #         self.val = val
  #         self.next = next
  class Solution:
	  def removeElements(self, head: ListNode, val: int) -> ListNode:
		  dummy = ListNode()
		  dummy.next = head
		  p = dummy
		  while p != None and p.next != None:
			  while p.next != None and p.next.val == val:
				  p.next = p.next.next
			  p = p.next
		  return dummy.next

```