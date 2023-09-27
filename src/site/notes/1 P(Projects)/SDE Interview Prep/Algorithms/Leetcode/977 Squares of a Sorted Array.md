---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/977-squares-of-a-sorted-array/","tags":["Leetcode/Easy","Leetcode/代码随想录"],"noteIcon":"1"}
---


## 题目信息

- 链接: [squares-of-a-sorted-array](https://leetcode.cn/problems/squares-of-a-sorted-array/)
- Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.
  
  Given an integer array `nums` sorted in **non-decreasing** order, return _an array of **the squares of each number** sorted in non-decreasing order_.
  
  **Example 1:**
  
  ```
  Input: nums = [-4,-1,0,3,10]
  Output: [0,1,9,16,100]
  Explanation: After squaring, the array becomes [16,1,0,9,100].
  After sorting, it becomes [0,1,9,16,100].
  
  ```
  
  **Example 2:**
  
  ```
  Input: nums = [-7,-3,2,3,11]
  Output: [4,9,9,49,121]
  
  ```
  
  **Constraints:**
	- `1 <= nums.length <= 10<sup>4</sup>`
	- `-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup>`
	- `nums` is sorted in **non-decreasing** order.
  
  **Follow up:** Squaring each element and sorting the new array is very trivial, could you find an `O(n)` solution using a different approach?

- 给你一个按 非递减顺序 排序的整数数组 nums，返回 每个数字的平方 组成的新数组，要求也按 非递减顺序 排序。
## 解题思路

- 暴力解法需要对平方后的数组排序，复杂度$O(nlogn)$
- 双指针法利用数组*并非完全无序*的特点，复杂度$O(n)$
- 关键: 平方后的最大值就在nums的两端，因为其绝对值大小为`大->小->大`
- 所以使用 [[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Two Pointers#首尾双指针｜首尾双指针\|Two Pointers#首尾双指针｜首尾双指针]] 两个指针i、j分别于nums的两端，每次比较i、j指向数的平方，将平方后大的放入result，并相应左右移动
## 代码

```python
  class Solution:
	  def sortedSquares(self, nums: List[int]) -> List[int]:
		  left = 0
		  right = len(nums)-1
		  result = [0] * len(nums)
		  curidx = len(nums)-1
		  while curidx >= 0:
			  if nums[left]*nums[left] < nums[right]*nums[right]:
				  result[curidx] = nums[right] * nums[right]
				  right -= 1
			  else:
				  result[curidx] = nums[left] * nums[left]
				  left += 1
			  curidx -= 1
		  return result
  ```