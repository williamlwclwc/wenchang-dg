---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/349-intersection-of-two-arrays/","tags":["Leetcode/Easy","Leetcode/代码随想录"],"noteIcon":"1"}
---

## 题目信息

- 链接: [intersection-of-two-arrays](https://leetcode.cn/problems/intersection-of-two-arrays/)
- Given two integer arrays `nums1` and `nums2`, return _an array of their intersection_. Each element in the result must be **unique** and you may return the result in **any order**.
  
  **Example 1:**
  
  ```
  Input: nums1 = [1,2,2,1], nums2 = [2,2]
  Output: [2]
  
  ```
  
  **Example 2:**
  
  ```
  Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
  Output: [9,4]
  Explanation: [4,9] is also accepted.
  
  ```
  
  **Constraints:**
	- `1 <= nums1.length, nums2.length <= 1000`
	- `0 <= nums1[i], nums2[i] <= 1000`
- 描述:
	- 给定两个数组  `nums1`  和  `nums2` ，返回_它们的交集_ 。输出结果中的每个元素一定是**唯一**的。我们可以**不考虑输出结果的顺序**。
## 解题思路

- 转成set取交集即可，set可以保证不重复和O(1)复杂度判断元素是否在set内
- 遍历全部num，找到即出现在nums1的元素又出现在nums2的num，放入result中
- 一行答案: `list(set(nums1) & set(nums2))`
## 代码

```python
  class Solution:
	  def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
		  result = []
		  nums = nums1 + nums2
		  nums1 = set(nums1)
		  nums2 = set(nums2)
		  nums = set(nums)
		  for num in nums:
			  if num in nums1 and num in nums2:
				  result.append(num)
		  return result
  ```