---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/24-swap-nodes-in-pairs/","tags":["Leetcode/Medium","Leetcode/代码随想录"],"noteIcon":"1"}
---

## 题目信息

- 链接: [swap-nodes-in-pairs](https://leetcode.cn/problems/swap-nodes-in-pairs/)
- Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)
  
  **Example 1:**
  
  ![](https://assets.leetcode.com/uploads/2020/10/03/swap_ex1.jpg)
  
  ```
  Input: head = [1,2,3,4]
  Output: [2,1,4,3]
  
  ```
  
  **Example 2:**
  
  ```
  Input: head = []
  Output: []
  
  ```
  
  **Example 3:**
  
  ```
  Input: head = [1]
  Output: [1]
  
  ```
  
  **Constraints:**
	- The number of nodes in the list is in the range `[0, 100]`.
	- `0 <= Node.val <= 100`

- 描述:
	- 给你一个链表，两两交换其中相邻的节点，并返回交换后链表的头节点。你必须在不修改节点内部的值的情况下完成本题（即，只能进行节点交换）

## 解题思路

- 正常模拟即可，涉及到头节点，最好使用 [[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Linked List#Dummy Node 哑巴/虚拟节点\|dummy node]]，最好画图方便理解
- ![image.png](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/24-fig1.png)
- ![image.png](https://raw.githubusercontent.com/williamlwclwc/Picgo-IHS/main/img/24-swap-fig2.png)
- 两两交换，加上前后两个节点一共影响4个节点，我们需要找到要**交换节点之前的节点**作为起点cur
	- `cur->n1->n2->n3` -> `cur->n2->n1->n3`
- 下一次交换n3和n4需要找到n3前面的节点，也就是交换后的n1，所以cur移动到n1
- 首先cur指向目标pairs之前的node, cur.next和cur.next.next都不能是None
	1. node1 = cur.next
	2. cur.next = cur.next.next
	3. node3 = cur.next.next
	4. cur.next.next = node1
	5. node1.next = node3
	6. cur = node1

## 代码

```python
	  # Definition for singly-linked list.
	  # class ListNode:
	  #     def __init__(self, val=0, next=None):
	  #         self.val = val
	  #         self.next = next
	  class Solution:
	      def swapPairs(self, head: ListNode) -> ListNode:
	          dummy = ListNode()
	          dummy.next = head
	          cur = dummy
	          while cur.next is not None and cur.next.next is not None:
	              node1 = cur.next
	              cur.next = cur.next.next
	              node3 = cur.next.next
	              cur.next.next = node1
	              node1.next = node3
	              cur = node1
	          return dummy.next
	  ```