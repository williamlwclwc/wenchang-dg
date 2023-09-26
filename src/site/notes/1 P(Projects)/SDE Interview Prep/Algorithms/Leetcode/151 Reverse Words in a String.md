---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/151-reverse-words-in-a-string/","tags":["Leetcode/Medium","Leetcode/代码随想录"],"noteIcon":"1"}
---


## 题目信息

- 链接: [reverse-words-in-a-string](https://leetcode.cn/problems/reverse-words-in-a-string/)
- Given an input string `s`, reverse the order of the **words**.
  
  A **word** is defined as a sequence of non-space characters. The **words** in `s` will be separated by at least one space.
  
  Return _a string of the words in reverse order concatenated by a single space._
  
  **Note** that `s` may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.
  
  **Example 1:**
  
  ```
  Input: s = "the sky is blue"
  Output: "blue is sky the"
  
  ```
  
  **Example 2:**
  
  ```
  Input: s = "  hello world  "
  Output: "world hello"
  Explanation: Your reversed string should not contain leading or trailing spaces.
  
  ```
  
  **Example 3:**
  
  ```
  Input: s = "a good   example"
  Output: "example good a"
  Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
  
  ```
  
  **Constraints:**
	- `1 <= s.length <= 10<sup>4</sup>`
	- `s` contains English letters (upper-case and lower-case), digits, and spaces `' '`.
	- There is **at least one** word in `s`.
  
  **Follow-up:** If the string data type is mutable in your language, can you solve it **in-place** with `O(1)` extra space?

- 描述:
	- 给你一个字符串 s ，颠倒字符串中 单词 的顺序。
	- 单词 是由非空格字符组成的字符串。s 中使用至少一个空格将字符串中的 单词 分隔开。
	- 返回 单词 顺序颠倒且 单词 之间用单个空格连接的结果字符串。
	- 注意：输入字符串 s中可能会存在前导空格、尾随空格或者单词间的多个空格。返回的结果字符串中，单词间应当仅用单个空格分隔，且不包含任何额外的空格。

## 解题思路

- Python可以直接用内置split、reverse、join快速解决，Python字符串不可变，所以空间复杂度至少是$O(n)$
- C/C++这类可以in-place操作字符串的语言可以用[[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Two Pointers\|Two Pointers]]达到空间复杂度O(1)，
	- 需要先 [[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Two Pointers#快慢指针\|快慢指针]] 去掉空格: 快指针遇到空格就继续，非空格时就把单词复制到慢指针的位置，到达s结尾或遇到空格代表单词结束，如果是C/C++最后需要resize一下s
	- 然后翻转全部字符: 使用首尾双指针依次交换即可
	- 最后反转每个单词: 一样还是通过s末尾或空格判断是否为一个单词
	- 参考 [[1 P(Projects)/SDE Interview Prep/Algorithms/Leetcode/27 Remove Element\|27 移除元素]]

## 代码

```python
  class Solution:
	  def reverseWords(self, s: str) -> str:
		  return ' '.join(reversed(s.split()))
	  ```