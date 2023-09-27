---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/209-minimum-size-subarray-sum/","tags":["Leetcode/Medium","Leetcode/代码随想录"],"noteIcon":"1"}
---


## 题目信息

- 链接: [minimum-size-subarray-sum](https://leetcode.cn/problems/minimum-size-subarray-sum/)
- Given an array of positive integers `nums` and a positive integer `target`, return _the **minimal length** of a subarray_
  
  _whose sum is greater than or equal to_ `target`. If there is no such subarray, return `0` instead.
  
  **Example 1:**
  
  ```
  Input: target = 7, nums = [2,3,1,2,4,3]
  Output: 2
  Explanation: The subarray [4,3] has the minimal length under the problem constraint.
  
  ```
  
  **Example 2:**
  
  ```
  Input: target = 4, nums = [1,4,4]
  Output: 1
  
  ```
  
  **Example 3:**
  
  ```
  Input: target = 11, nums = [1,1,1,1,1,1,1,1]
  Output: 0
  
  ```
  
  **Constraints:**
	- `1 <= target <= 10<sup>9</sup>`
	- `1 <= nums.length <= 10<sup>5</sup>`
	- `1 <= nums[i] <= 10<sup>4</sup>`
  
  **Follow up:** If you have figured out the `O(n)` solution, try coding another solution of which the time complexity is `O(n log(n))`.

- 描述:
	- 给定一个含有 n 个正整数的数组和一个正整数 target 。
	- 找出该数组中满足其和 ≥ target 的长度最小的连续子数组 [numsl, numsl+1, ..., numsr-1, numsr] ，并返回其长度。如果不存在符合条件的子数组，返回 0 。

## 解题思路

- 暴力搜索: $O(n^2)$遍历所有的子数组找到符合条件的
- [[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Sliding Window\|滑动窗口]]法: $O(n)$ 因为要求*连续子数组*，想到可以用滑动窗口
	- 使用左边界i、右边界j，一开始都在0处，子数组和小于等于target就让j右移，和大于target就让左边界左移。当和等于target时，更新最小长度
	- 如果最小长度没被更新过就返回0，否则返回最小长度

## 代码

```python
  class Solution:
	  def minSubArrayLen(self, target: int, nums: List[int]) -> int:
		  minLen = float('inf')
		  i, j = 0, 0
		  curSum = 0
		  while j <= len(nums):
			  if curSum <= target:
				  if j < len(nums):
					  curSum += nums[j]
				  j += 1
			  else:
				  curSum -= nums[i]
				  i += 1
			  if curSum >= target:
				  if j - i < minLen:
					  minLen = j - i
		  if minLen == float('inf'):
			  return 0
		  else:
			  return minLen
	  ```