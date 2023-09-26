---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/316-remove-duplicate-letters/","tags":["Leetcode/Medium","#Huawei-VO"],"noteIcon":"1"}
---


## 题目信息

- 链接: https://leetcode.cn/problems/remove-duplicate-letters/
- Given a string `s`, remove duplicate letters so that every letter appears once and only once. You must make sure your result is **the smallest in lexicographical order** among all possible results.
  
  **Example 1:**
  
  ```
  Input: s = "bcabc"
  Output: "abc"
  
  ```
  
  **Example 2:**
  
  ```
  Input: s = "cbacdcbc"
  Output: "acdb"
  
  ```
  
  **Constraints:**
	- `1 <= s.length <= 10<sup>4</sup>`
	- `s` consists of lowercase English letters.
  
  **Note:** This question is the same as 1081: [https://leetcode.com/problems/smallest-subsequence-of-distinct-characters/](https://leetcode.com/problems/smallest-subsequence-of-distinct-characters/)

## 解题思路

- 首先需要理解题意: 首先要保证去掉重复的字母，如果有多种方式则选择字典序最小的
- 排除重复字母比较容易，我们只需要遍历一次就可以知道每个字母的位置以及出现次数，但是保证最小字典序就需要用到 [单调栈]([[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Monotonic Stack\|Monotonic Stack]]) 的数据结构
- 我们遍历字符串s，对于每一个字母，我们先加入单调栈中，如果字典序新加入的字母比栈顶的小，那么:
	- 我们首先要判断，前面的字母在后面未遍历的部分有没有出现，如果没有出现，那么这个字母必须保留
	- 如果后面有出现，那么这个栈顶字母就可以出栈不要了
	- 这样我们有了一个字典序的单调栈，不过如果有字母在后面没出现，则是一个分段字典序单调的单调栈
- 最后只需要把单调栈list转换成字符串return即可
- 过程中我们需要判断栈顶字符后面是否出现过，所以我们需要 [[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Hashmap\|哈希表]] 先遍历一次把字母最后一次出现位置存下来
- 同时如果出现 `aba` 类似的情况，我们需要保证后一个a不添加，也不能把b给pop出来。所以需要对每个遍历的字母检查是否已经在单调栈中出现过，这里也需要一个hashset来保存mono_stack中存在的字母

## 代码

```python
  class Solution:
	  def removeDuplicateLetters(self, s: str) -> str:
		  mono_stack = []
		  app_dict = {} # char : largest idx of that char
		  cur_set = set() # make sure not adding existed char
		  for i in range(len(s)):
			  app_dict[s[i]] = i
		  for i in range(len(s)):
			  # check if new added char already existed
			  if s[i] in cur_set:
				  continue
			  while mono_stack and s[i] < mono_stack[-1]:
				  # check if mono_stack[-1] appears later
				  if app_dict[mono_stack[-1]] >= i:
					  cur_set.remove(mono_stack[-1])
					  mono_stack.pop()
				  else:
					  break
			  mono_stack.append(s[i])
			  cur_set.add(s[i])
		  return "".join(mono_stack)
	  
	  ```