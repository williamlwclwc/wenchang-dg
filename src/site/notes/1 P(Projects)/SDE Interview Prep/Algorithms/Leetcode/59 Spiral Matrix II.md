---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/leetcode/59-spiral-matrix-ii/","tags":["Leetcode/Medium","Leetcode/代码随想录"],"noteIcon":"1"}
---

## 题目信息

- 链接: [spiral-matrix-ii](https://leetcode.cn/problems/spiral-matrix-ii/)
- Given a positive integer `n`, generate an `n x n` `matrix` filled with elements from `1` to `n<sup>2</sup>` in spiral order.
  
  **Example 1:**
  
  ![](https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg)
  
  ```
  Input: n = 3
  Output: [[1,2,3],[8,9,4],[7,6,5]]
  
  ```
  
  **Example 2:**
  
  ```
  Input: n = 1
  Output: [[1]]
  
  ```
  
  **Constraints:**
	- `1 <= n <= 20`

- 描述:
	- 给你一个正整数 n ，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的 n x n 正方形矩阵 matrix 。

## 解题思路

- 没有什么技巧，关键是判断*什么时候改变方向*: **碰到边界或者之前已经填入数字的位置**
- 先从左到右开始依次填入 $n \times n$ 矩阵，遇到右边界向下走，遇到下边界向左走，遇到左边界向上走，遇到上边界向右走
- 循环 $n\times n$ 次，每次填入一个数，将坐标移动到下一个位置，如果这个位置超出了边界或者已经填入过其他数，那么就改变方向(右->下->左->上->右)

## 代码
 
```python
	  class Solution:
	      def generateMatrix(self, n: int) -> List[List[int]]:
	          result = [[-1] * n for _ in range(n)]
	          # dir: 0 right, 1 down, 2 left, 3 up
	          direction = 0
	          x, y = 0, 0
	          for i in range(1, n*n+1):
	              result[x][y] = i
	              if direction == 0:
	                  y += 1
	                  if y >= n or result[x][y] != -1:
	                      y -= 1
	                      direction = 1
	                      x += 1
	              elif direction == 1:
	                  x += 1
	                  if x >= n or result[x][y] != -1:
	                      x -= 1
	                      direction = 2
	                      y -= 1
	              elif direction == 2:
	                  y -= 1
	                  if y < 0 or result[x][y] != -1:
	                      y += 1
	                      direction = 3
	                      x -= 1
	              elif direction == 3:
	                  x -= 1
	                  if x < 0 or result[x][y] != -1:
	                      x += 1
	                      direction = 0
	                      y += 1
	              # print(result)
	          return result
	  ```