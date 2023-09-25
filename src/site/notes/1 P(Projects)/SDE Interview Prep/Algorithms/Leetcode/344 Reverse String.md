---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/344-reverse-string/","tags":["Leetcode/Easy","Leetcode/代码随想录"],"noteIcon":"1"}
---


## 题目信息

- 链接: [reverse-string](https://leetcode.cn/problems/reverse-string/)
- Write a function that reverses a string. The input string is given as an array of characters `s`.
  
  You must do this by modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) with `O(1)` extra memory.
  
  **Example 1:**
  
  ```
  Input: s = ["h","e","l","l","o"]
  Output: ["o","l","l","e","h"]
  
  ```
  
  **Example 2:**
  
  ```
  Input: s = ["H","a","n","n","a","h"]
  Output: ["h","a","n","n","a","H"]
  
  ```
  
  **Constraints:**
- `1 <= s.length <= 10<sup>5</sup>`
- `s[i]` is a [printable ascii character](https://en.wikipedia.org/wiki/ASCII#Printable_characters).
- 描述:
	- 编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 s 的形式给出。
	- 不要给另外的数组分配额外的空间，你必须原地修改输入数组、使用 O(1) 的额外空间解决这一问题


## 解题思路

- [[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Two Pointers#首尾双指针\|Two Pointers#首尾双指针]]，头尾交换元素，left右移，right左移，直到left、right相遇

## 代码

 ```python
  class Solution:
	  def reverseString(self, s: List[str]) -> None:
		  """
		  Do not return anything, modify s in-place instead.
		  """
		  left = 0
		  right = len(s)-1
		  while left < right:
			  # swap l, r
			  temp = s[left]
			  s[left] = s[right]
			  s[right] = temp
			  # move left, right
			  left += 1
			  right -= 1	  
```
