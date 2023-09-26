---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/206-reverse-linked-list/","tags":["Leetcode/Easy","Leetcode/Hot100","Leetcode/Blind75","Leetcode/代码随想录","Leetcode/Neetcode150"],"noteIcon":"1"}
---

## 题目信息

- 链接: [reverse-linked-list](https://leetcode-cn.com/problems/reverse-linked-list/)
- Given the `head` of a singly linked list, reverse the list, and return _the reversed list_.
  
  **Example 1:**
  
  ![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)
  
  ```
  Input: head = [1,2,3,4,5]
  Output: [5,4,3,2,1]
  
  ```
  
  **Example 2:**
  
  ![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)
  
  ```
  Input: head = [1,2]
  Output: [2,1]
  
  ```
  
  **Example 3:**
  
  ```
  Input: head = []
  Output: []
  
  ```
  
  **Constraints:**
	- The number of nodes in the list is the range `[0, 5000]`.
	- `-5000 <= Node.val <= 5000`
  
  **Follow up:** A linked list can be reversed either iteratively or recursively. Could you implement both?

- 描述:
	- 给你单链表的头节点 head ，请你反转链表，并返回反转后的链表。

## 解题思路

- [[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Two Pointers\|双指针]]: 假设当前节点为p，前面的节点为prev
	- 首先保存p.next为next，p.next指向prev
	- prev指向p，p指向next
- [[Recursion\|递归]]: 和遍历法基本一样，pre和p后移遍历变成了递归pre和p，更抽象并且空间复杂度更高，不推荐

## 代码
### Iteratively

```python
  # Definition for singly-linked list.
  # class ListNode:
  #     def __init__(self, val=0, next=None):
  #         self.val = val
  #         self.next = next
  class Solution:
	  def reverseList(self, head: ListNode) -> ListNode:
		  if head == None:
			  return None
		  p = head
		  prev = None
		  while p != None:
			  n = p.next
			  p.next = prev
			  prev = p
			  p = n
		  return prev
  ```

### Recursively

```python
  # Definition for singly-linked list.
  # class ListNode:
  #     def __init__(self, val=0, next=None):
  #         self.val = val
  #         self.next = next
  class Solution:
	  def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
		  def _reverse(prev, cur):
			  if cur is None:
				  return prev
			  tmp = cur.next
			  cur.next = prev
			  prev = cur
			  return _reverse(prev, tmp)
  
		  return _reverse(None, head)
  ```