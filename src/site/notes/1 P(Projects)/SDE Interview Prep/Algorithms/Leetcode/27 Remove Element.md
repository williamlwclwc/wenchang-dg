---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/27-remove-element/","tags":["Leetcode/Easy","Leetcode/代码随想录"],"noteIcon":"1"}
---


## 题目信息

- 链接: [remove-element](https://leetcode.cn/problems/remove-element/)

- Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm). The order of the elements may be changed. Then return _the number of elements in_ `nums` _which are not equal to_ `val`.
  
- Consider the number of elements in `nums` which are not equal to `val` be `k`, to get accepted, you need to do the following things:
	- Change the array `nums` such that the first `k` elements of `nums` contain the elements which are not equal to `val`. The remaining elements of `nums` are not important as well as the size of `nums`.
	- Return `k`.
  
  **Custom Judge:**
  
  The judge will test your solution with the following code:
  
  ```
  int[] nums = [...]; // Input array
  int val = ...; // Value to remove
  int[] expectedNums = [...]; // The expected answer with correct length.
							// It is sorted with no values equaling val.
  
  int k = removeElement(nums, val); // Calls your implementation
  
  assert k == expectedNums.length;
  sort(nums, 0, k); // Sort the first k elements of nums
  for (int i = 0; i < actualLength; i++) {
	assert nums[i] == expectedNums[i];
  }
  
  ```
  
  If all assertions pass, then your solution will be **accepted**.
  
  **Example 1:**
  
  ```
  Input: nums = [3,2,2,3], val = 3
  Output: 2, nums = [2,2,_,_]
  Explanation: Your function should return k = 2, with the first two elements of nums being 2.
  It does not matter what you leave beyond the returned k (hence they are underscores).
  
  ```
  
  **Example 2:**
  
  ```
  Input: nums = [0,1,2,2,3,0,4,2], val = 2
  Output: 5, nums = [0,1,4,0,3,_,_,_]
  Explanation: Your function should return k = 5, with the first five elements of nums containing 0, 0, 1, 3, and 4.
  Note that the five elements can be returned in any order.
  It does not matter what you leave beyond the returned k (hence they are underscores).
  
  ```
  
  **Constraints:**
- `0 <= nums.length <= 100`
- `0 <= nums[i] <= 50`
- `0 <= val <= 100`
- 给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度。
- 不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并 原地 修改输入数组。
- 元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

## 解题思路

- 暴力双循环时间复杂度 $O(n^2)$
- [[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Two Pointers#快慢指针\|快慢指针]] 时间复杂度 $O(n)$，空间复杂度$O(1)$ 
- 假设要删除的元素为n，一开始快慢指针一起从0位置开始右移，快指针遇到n之后就右移跳过n，指到非n的元素，如果快慢指针指向元素不相同，就把快指针指向元素(非n)复制到慢指针指向位置
- 直到快指针走到 `len(nums)`，返回慢指针index

## 代码

```python
  class Solution:
	  def removeElement(self, nums: List[int], val: int) -> int:
		  slow, fast = 0, 0
		  while fast < len(nums):
			  while nums[fast] == val:
				  fast += 1
				  if fast >= len(nums):
					  return slow
			  if nums[fast] != nums[slow]:
				  nums[slow] = nums[fast]
			  fast += 1
			  slow += 1
		  return slow
  ```
