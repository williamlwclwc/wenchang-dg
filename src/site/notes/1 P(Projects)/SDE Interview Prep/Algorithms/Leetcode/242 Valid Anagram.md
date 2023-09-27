---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/242-valid-anagram/","tags":["Leetcode/Easy","Leetcode/代码随想录","Leetcode/Blind75"],"noteIcon":"1"}
---

## 题目信息

- 链接: [valid-anagram](https://leetcode.cn/problems/valid-anagram/)
- Given two strings `s` and `t`, return `true` _if_ `t` _is an anagram of_ `s`_, and_ `false` _otherwise_.
  
  An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.
  
  **Example 1:**
  
  ```
  Input: s = "anagram", t = "nagaram"
  Output: true
  
  ```
  
  **Example 2:**
  
  ```
  Input: s = "rat", t = "car"
  Output: false
  
  ```
  
  **Constraints:**
	- `1 <= s.length, t.length <= 5 * 10<sup>4</sup>`
	- `s` and `t` consist of lowercase English letters.
  
  **Follow up:** What if the inputs contain Unicode characters? How would you adapt your solution to such a case?
- 描述:
	- 给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。
	- 注意：若 s 和 t 中每个字符出现的次数都相同，则称 s 和 t 互为字母异位词

## 解题思路

- 遍历s，用哈希表存下每个字母在s出现的次数
- 遍历t，如果存在哈希表没有的字符return False，如果遇到出现的字符则记录次数-1
- 遍历哈希表，如果所有字符对应次数都减为0说明s、t字符出现次数相同return True，否则return False
	- 如果不想最后遍历哈希表，可以在遍历t过程中检查是否有次数为负，另外还需要检查s和t长度，否则可能有字母次数没用完的情况，而 [[1 P(Projects)/SDE Interview Prep/Algorithms/Leetcode/383 Ransom Note\|383 赎金信]] 没有用完也可以
- 注: 由于都是字母小写，也可以使用[[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Array\|数组]]来代替哈希表，不过如果出现其他unicode字符就不好办了

## 代码

### 常规思路

```python
  class Solution:
	  def isAnagram(self, s: str, t: str) -> bool:
		  anagram_dict = {}
		  for char in s:
			  if anagram_dict.get(char) is None:
				  anagram_dict[char] = 1
			  else:
				  anagram_dict[char] += 1
		  for char in t:
			  if anagram_dict.get(char) is None:
				  return False
			  else:
				  anagram_dict[char] -= 1
		  for key, value in anagram_dict.items():
			  if value != 0:
				  return False
		  return True
	  ```

### 不需要最后遍历哈希表

```python
  class Solution:
	  def isAnagram(self, s: str, t: str) -> bool:
		  if len(s) != len(t):
			  return False
			  
		  f_dict = {}
		  for char in s:
			  if f_dict.get(char):
				  f_dict[char] += 1
			  else:
				  f_dict[char] = 1
		  
		  for char in t:
			  if f_dict.get(char):
				  f_dict[char] -= 1
				  if f_dict[char] < 0:
					  return False
			  else:
				  return False
		  
		  return True
	  ```