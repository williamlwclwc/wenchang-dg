---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/topics/binary-search/","tags":["Leetcode/Algo"],"noteIcon":"1"}
---

## Binary Search 

- 通常在有序[[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Array\|数组]]上进行，如果无序则需要先对数组进行[[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Sort\|排序]], 时间复杂度$O(nlogn)$
- 二分搜索的思路就是通过*比较搜索空间的中间值和给定目标值*，每次去掉一半的搜索范围，实现比线性查找更快的搜索，复杂度$O(logn)$

### 搜索思路

- 因为数组是排好序的，所以如果数组的某个区间内，其中间值已经大于给定目标，则说明中间值往右的值(比中间值更大)肯定也大于目标，所以我们可以去掉中间值往右的搜索区间；同理，如果中间值比目标小，那么中间值往左的值肯定也小于目标，所以我们可以去掉中间值往左的搜索区间；如果运气好中间值和目标值相等那么直接return
- 如果搜索空间已经被去掉的没有剩余值了，我们仍然没能return，那么就说明目标值不存在
- 所以每次搜索我们必定可以做到以下之一，从而保证$O(logn)$的复杂度: 
	- 去掉mid左边的搜索空间 
	- 去掉mid右边的搜索空间
	- 找到target
- 根据搜索区间的定义不同，实现上也略有不同，一般分为*左闭右闭*和*左闭右开*两种

#### 左闭右闭(更推荐)

- 指排除掉的搜索区间包含左右端点值，即下一个搜索空间不会包含这次的中间值mid
- 因为搜索区间包含两个端点值，所以`left==right`时区间依然有值，判断条件为`left <= right`
- 右端点初始值为`len(nums)-1`，因为包含的右端点值得存在

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums)-1
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] < target:
                left = mid + 1
            elif nums[mid] > target:
                right = mid - 1
            else:
                return mid
        return -1 
```

#### 左闭右开

- 指排除掉的搜索区间不包含右端点值，即这次的中间值mid依然包含在下一个搜索区间内
- 因为搜索区间不包含右端点，所以`left==right`时区间没有可用的值，判断条件为`left < right`
- 因为不包含右端点，所以右端点初始值为`len(num)`，并不存在

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums)
        while left < right:
            mid = (left + right) // 2
            if nums[mid] < target:
                left = mid + 1
            elif nums[mid] > target:
                right = mid
            else:
                return mid
        return -1 
```

