---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/454-4-sum-ii/","tags":["Leetcode/Medium","Leetcode/代码随想录"],"noteIcon":"1"}
---

## 题目信息

- 链接: [4sum-ii](https://leetcode.cn/problems/4sum-ii/)
- Given four integer arrays `nums1`, `nums2`, `nums3`, and `nums4` all of length `n`, return the number of tuples `(i, j, k, l)` such that:
	- `0 <= i, j, k, l < n`
	- `nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0`
  
  **Example 1:**
  
  ```
  Input: nums1 = [1,2], nums2 = [-2,-1], nums3 = [-1,2], nums4 = [0,2]
  Output: 2
  Explanation:
  The two tuples are:
  1. (0, 0, 0, 1) -> nums1[0] + nums2[0] + nums3[0] + nums4[1] = 1 + (-2) + (-1) + 2 = 0
  2. (1, 1, 0, 0) -> nums1[1] + nums2[1] + nums3[0] + nums4[0] = 2 + (-1) + (-1) + 0 = 0
  
  ```
  
  **Example 2:**
  
  ```
  Input: nums1 = [0], nums2 = [0], nums3 = [0], nums4 = [0]
  Output: 1
  
  ```
  
  **Constraints:**
	- `n == nums1.length`
	- `n == nums2.length`
	- `n == nums3.length`
	- `n == nums4.length`
	- `1 <= n <= 200`
	- `-2<sup>28</sup> <= nums1[i], nums2[i], nums3[i], nums4[i] <= 2<sup>28</sup>`
- 描述:
	- 给你四个整数数组 nums1、nums2、nums3 和 nums4 ，数组长度都是 n ，请你计算有多少个元组 (i, j, k, l) 能满足：
	- 0 <= i, j, k, l < n
	  `nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0`

## 解题思路

- 暴力法循环4个数组$O(n^4)$，使用哈希表可以优化到$O(n^2)$
- 将4个数组两两分组，遍历第一组所有的a+b和，并构建哈希表key为a+b，value为a+b出现的次数
- 遍历第二组c+d，在哈希表查找0-c-d，获得其出现次数value，cnt+=value

## 代码

```python
  class Solution:
	  def fourSumCount(self, nums1: List[int], nums2: List[int], nums3: List[int], nums4: List[int]) -> int:
		  s_dict = {}
		  result = 0
		  for a in nums1:
			  for b in nums2:
					  s_dict[a+b] = s_dict.get(a+b, 0) + 1
		  for c in nums3:
			  for d in nums4:
				  value = s_dict.get(0-c-d)
				  if value:
					  result += value
		  return result
  ```