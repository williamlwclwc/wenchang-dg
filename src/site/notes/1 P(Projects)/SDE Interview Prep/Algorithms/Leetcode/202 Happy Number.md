---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/202-happy-number/","tags":["Leetcode/Easy","Leetcode/代码随想录","Leetcode/Neetcode150"],"noteIcon":"1"}
---

## 题目信息

- 链接: [happy-number](https://leetcode.cn/problems/happy-number/)
- Write an algorithm to determine if a number `n` is happy.
  
  A **happy number** is a number defined by the following process:
	- Starting with any positive integer, replace the number by the sum of the squares of its digits.
	- Repeat the process until the number equals 1 (where it will stay), or it **loops endlessly in a cycle** which does not include 1.
	- Those numbers for which this process **ends in 1** are happy.
	  
	  Return `true` _if_ `n` _is a happy number, and_ `false` _if not_.
	  
	  **Example 1:**
	  
	  ```
	  Input: n = 19
	  Output: true
	  Explanation:
	  12 + 92 = 82
	  82 + 22 = 68
	  62 + 82 = 100
	  12 + 02 + 02 = 1
	  
	  ```
	  
	  **Example 2:**
	  
	  ```
	  Input: n = 2
	  Output: false
	  
	  ```
	  
	  **Constraints:**
		- `1 <= n <= 2<sup>31</sup> - 1`
- 描述:
	- 编写一个算法来判断一个数 n 是不是快乐数。
	- 「快乐数」 定义为：
	- 对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和。
	  然后重复这个过程直到这个数变为 1，也可能是 无限循环 但始终变不到 1。
	  如果这个过程 结果为 1，那么这个数就是快乐数。
	  如果 n 是 快乐数 就返回 true ；不是，则返回 false

## 解题思路

- 按照题目描述循环操作直到得到1为止即可，问题在于如何判断会不会出现无限循环。
- 简单的思路就是把每次得到的新n存入哈希表，如果发现重复出现n就表示出现了循环
- 不断除以10和取余就可以[[5 Inbox/得到一个数每个位置的数字\|得到一个数每个位置的数字]]
- 如果不允许使用额外空间，可以使用 [[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Two Pointers#快慢指针\|快慢指针]] 的方式。具体来说就是fast每回合多做一次sum square digits，如果fast和slow算出同一个结果说明会出现循环

## 代码

### With Hashset or Hashtable

```python
  class Solution:
	  def isHappy(self, n: int) -> bool:
		  cache = {}
		  while n != 1:
			  s = 0
			  while n != 0:
				  a = n % 10
				  s += a * a
				  n = n // 10
			  if s == 1:
				  return True
			  if cache.get(s) is not None:
				  return False
			  else:
				  cache[s] = 1
			  n = s
		  return True
	  ```

### Without Hashset

```python
  # from neetcode.io
  class Solution:
	  def isHappy(self, n: int) -> bool:
		  slow, fast = n, self.sumSquareDigits(n)
  
		  while slow != fast:
			  fast = self.sumSquareDigits(fast)
			  fast = self.sumSquareDigits(fast)
			  slow = self.sumSquareDigits(slow)
  
		  return True if fast == 1 else False
  
	  def sumSquareDigits(self, n):
		  output = 0
		  while n:
			  output += (n % 10) ** 2
			  n = n // 10
		  return output
  
  ```