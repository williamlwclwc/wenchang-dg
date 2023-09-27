---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/1-two-sum/","tags":["Leetcode/Easy","Leetcode/代码随想录","Leetcode/Blind75","Leetcode/Hot100"],"noteIcon":"1"}
---

## 题目信息

- 链接: [two-sum](https://leetcode-cn.com/problems/two-sum/)
- 给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。
- 你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。
- 你可以按任意顺序返回答案。
- Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_.
  
  You may assume that each input would have **_exactly_ one solution**, and you may not use the _same_ element twice.
  
  You can return the answer in any order.
  
  **Example 1:**
  
  ```
  Input: nums = [2,7,11,15], target = 9
  Output: [0,1]
  Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
  
  ```
  
  **Example 2:**
  
  ```
  Input: nums = [3,2,4], target = 6
  Output: [1,2]
  
  ```
  
  **Example 3:**
  
  ```
  Input: nums = [3,3], target = 6
  Output: [0,1]
  
  ```
  
  **Constraints:**
- `2 <= nums.length <= 10<sup>4</sup>`
- `-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup>`
- `-10<sup>9</sup> <= target <= 10<sup>9</sup>`
- **Only one valid answer exists.**
  
  **Follow-up:** Can you come up with an algorithm that is less than `O(n<sup>2</sup>)` time complexity?

## 解题思路

- 找到数组中两个数和为target，双循环可以轻松解决，但是能否小于$O(n^2)$?
- 使用[[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Hashmap\|哈希表]]可以用两次$O(n)$复杂度的搜索解决
	- 第一次哈希表记录每个数对应下标，目的是能通过`key=数`来找到下标i
	- 第二次遍历nums，对每个num，在哈希表检索`target-num`，如果存在就可以获得下表j，和num遍历下标i一起return即可
- 需要注意的是如果target是偶数而target/2有正好在nums中，那么很可能会return其下标两次，比如 `target=6`，`nums=[3, 4, 2]`。所以为了避免得到 `[0, 0]` 要加上判断num和target-num不能相同
- 除了哈希表还可以先排序[[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Sort\|排序]]，然后就和 [[1 P(Projects)/SDE Interview Prep/Algorithms/Leetcode/167 Two Sum II - Input Array is Sorted\|167 Two Sum II - Input Array is Sorted]] 一样了
 
## 代码

```python
  class Solution:
	  def twoSum(self, nums: List[int], target: int) -> List[int]:
		  num_d = {}
		  for i in range(len(nums)):
			  num_d[nums[i]] = i
		  for i in range(len(nums)):
			  if num_d.get(target-nums[i]) and \
				  i != num_d[target-nums[i]]:
				  return [i, num_d[target-nums[i]]]
  ```