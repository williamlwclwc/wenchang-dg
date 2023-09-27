---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/383-ransom-note/","tags":["Leetcode/Easy","Leetcode/代码随想录"],"noteIcon":"1"}
---

## 题目信息

- 链接: [ransom-note](https://leetcode.cn/problems/ransom-note/)
- Given two strings `ransomNote` and `magazine`, return `true` _if_ `ransomNote` _can be constructed by using the letters from_ `magazine` _and_ `false` _otherwise_.
  
  Each letter in `magazine` can only be used once in `ransomNote`.
  
  **Example 1:**
  
  ```
  Input: ransomNote = "a", magazine = "b"
  Output: false
  
  ```
  
  **Example 2:**
  
  ```
  Input: ransomNote = "aa", magazine = "ab"
  Output: false
  
  ```
  
  **Example 3:**
  
  ```
  Input: ransomNote = "aa", magazine = "aab"
  Output: true
  
  ```
  
  **Constraints:**
	- `1 <= ransomNote.length, magazine.length <= 10<sup>5</sup>`
	- `ransomNote` and `magazine` consist of lowercase English letters.

- 描述:
	- 给你两个字符串：ransomNote 和 magazine ，判断 ransomNote 能不能由 magazine 里面的字符构成。
	- 如果可以，返回 true ；否则返回 false 。
	- magazine 中的每个字符只能在 ransomNote 中使用一次。

## 解题思路

- 只需要将magazine转化为一个哈希表即可，key为字母，value为该字母出现的次数
- 遍历ransomNote时，return False条件为ransomNote中的字母magazine里没有，或magazine该字母可使用次数已经为0，否则最后就return True
- 因为字母数量有限，也可以使用数组来代替哈希表
- 和 [[1 P(Projects)/SDE Interview Prep/Algorithms/Leetcode/242 Valid Anagram\|242 有效的字母异位词]] 不同的是，前者要求相互可以组成，本题只要求magazine能组成ransomNote，也就是说magazine可以有些字符不使用
 
## 代码

```python
  class Solution:
	  def canConstruct(self, ransomNote: str, magazine: str) -> bool:
		  m_dict = {}
		  for c in magazine:
			  if m_dict.get(c) is None:
				  m_dict[c] = 1
			  else:
				  m_dict[c] += 1
		  for c in ransomNote:
			  if m_dict.get(c) is None:
				  return False
			  else:
				  if m_dict[c] == 0:
					  return False
				  else:
					  m_dict[c] -= 1
		  return True
  ```