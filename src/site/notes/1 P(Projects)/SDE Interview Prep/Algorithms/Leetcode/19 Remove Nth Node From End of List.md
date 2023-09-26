---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/19-remove-nth-node-from-end-of-list/","tags":["Leetcode/Medium","Leetcode/Hot100","Leetcode/Blind75","Leetcode/代码随想录"],"noteIcon":"1"}
---

- ## 题目信息
- 链接: [remove-nth-node-from-end-of-list](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)
- Given the `head` of a linked list, remove the `n<sup>th</sup>` node from the end of the list and return its head.
  
  **Example 1:**
  
  ![](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)
  
  ```
  Input: head = [1,2,3,4,5], n = 2
  Output: [1,2,3,5]
  
  ```
  
  **Example 2:**
  
  ```
  Input: head = [1], n = 1
  Output: []
  
  ```
  
  **Example 3:**
  
  ```
  Input: head = [1,2], n = 1
  Output: [1]
  
  ```
  
  **Constraints:**
	- The number of nodes in the list is `sz`.
	- `1 <= sz <= 30`
	- `0 <= Node.val <= 100`
	- `1 <= n <= sz`
  
  **Follow up:** Could you do this in one pass?

- 描述:
	- 给你一个链表，删除链表的倒数第 n 个结点，并且返回链表的头结点。

## 解题思路

- 想要删除倒数第N个结点，只需要获取倒数第N+1个结点的指针p即可完成链表删除操作

### 计算链表长度(容易想到)

- 假设链表总长度为L，倒数第N个结点就是正数第 `L-N+1` 个结点，我们需要的p就是正数第 `L-N` 个结点

### 快慢指针

- 分别使用快指针fast和慢指针slow，fast先遍历到N+1个结点，之和和在头结点的slow同时开始遍历，当fast到链表尾时，slow就处在倒数第N+1个结点了
- 相当于fast先走了N+1，这样fast到终点时，slow距离终点还差N+1，即slow处在倒数N+1个节点的位置

### 删除链表节点

- 删除p的下一个结点: `p.next = p.next.next`
- 另外需要注意如果需要移除头结点可以使用 [[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Linked List#Dummy Node 哑巴/虚拟节点\|Dummy Node]] 

## 代码

### 计算链表长度

```python
  # class ListNode:
  #     def __init__(self, val=0, next=None):
  #         self.val = val
  #         self.next = next
  class Solution:
	  def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
		  p = head
		  l = 0
		  # get the length of the linked list L
		  while p != None:
			  l += 1
			  p = p.next
		  # find the L-N node's pointer
		  # then remove the L-N+1 node
		  if l-n == 0:
			  # if l-n == 0, remove head node
			  dummy = ListNode()
			  dummy.next = head
			  p = dummy
			  p.next = p.next.next
			  return dummy.next
		  cnt = 0
		  p = head
		  while p != None:
			  cnt += 1
			  if cnt == l-n:
				  # current p points to L-N
				  p.next = p.next.next
				  break
			  p = p.next
		  return head
	  
	  ```

### 快慢指针

```python
  # Definition for singly-linked list.
  # class ListNode:
  #     def __init__(self, val=0, next=None):
  #         self.val = val
  #         self.next = next
  class Solution:
	  def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
		  # find (N+1)th from the end of the list
		  dummy = ListNode(next=head)
		  fast, slow = dummy, dummy
		  # fast pointer start from n+1 nodes ahead
		  for _ in range(n+1):
			  fast = fast.next
		  # slow is the target node when fast points to the end
		  while fast is not None:
			  slow = slow.next
			  fast = fast.next
		  # remove node
		  # n>=1 slow is at least the 2nd node from the end, slow.next will not be None
		  slow.next = slow.next.next
		  return dummy.next 

```