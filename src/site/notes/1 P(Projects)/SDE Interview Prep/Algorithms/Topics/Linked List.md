---
{"dg-publish":true,"permalink":"/1-p-projects/sde-interview-prep/algorithms/topics/linked-list/","tags":["Leetcode/DS"],"noteIcon":"1"}
---

## Linked List 链表

- What is a linked list?
	- Linear data structure
	- Consists of Nodes: data + next pointer
	- Not contiguous in Memory, unlike [[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Array\|Array]]
- Different Types of Linked Lists:
	- Singly Linked List 单链表: 只有一个指针pointer，遍历方向也是单向的，只能前往下一个节点
	- Doubly Linked List 双链表: 有两个指针，一般一个指向next一个previous，可以实现双向遍历，前往下一个节点或上一个节点
	- Circular Linked List 循环链表: 链表中存在环，首尾相接

### Definition 链表定义

```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

test_node = ListNode(0)
```

```C++
// 单链表
struct ListNode {
    int val;  // 节点上存储的元素
    ListNode *next;  // 指向下一个节点的指针
    ListNode(int x) : val(x), next(NULL) {}  // 节点的构造函数
};

ListNode* head = new ListNode(5);
```

```JavaScript
class ListNode {
  val;
  next = null;
  constructor(value) {
    this.val = value;
    this.next = null;
  }
}
```

### 注意空指针

- 遍历中注意null/nil/NULL/None等值，如果访问这些值的指针就会出错
- 尤其注意边界值，None.next就会出错

## 基础操作

- [[1 P(Projects)/SDE Interview Prep/Algorithms/Leetcode/707 Design Linked List\|707 Design Linked List]] 涵盖大部分基础操作
- [[1 P(Projects)/SDE Interview Prep/Algorithms/Leetcode/24 Swap Nodes in Pairs\|24 Swap Nodes in Pairs]] 较比复杂的链表操作
### 添加节点

![链表-添加节点](https://code-thinking-1253855093.file.myqcloud.com/pics/20200806195134331-20230310121503147.png)

```python
# 单链表插入 prev(C) new(F) C -> F -> D
new.next = prev.next # F->D
prev.next = new # C->F
```

```python
# 双向链表插入 
new.next = a.next 
new.prev = b.prev
a.next = new
b.prev = new
```

- 因为插入节点会导致两个节点之前的链接断开，所以需要先处理new.next和new.prev。之前再处理a.next和b.prev

### 删除节点

![链表-删除节点](https://code-thinking-1253855093.file.myqcloud.com/pics/20200806195114541-20230310121459257.png)

- 只需要链接跳过removed即可，如果没有垃圾回收(如C/C++)需要手动释放空间
- 单链表删除
	- `prev.next = removed.next`
- 双向链表删除
	- `a.next = removed.next`
	- `b.prev = removed.prev`

### 时间复杂度 

- 链表插入和删除复杂度都是$O(1)$，因为不需要移动其他元素
- 链表查询复杂度$O(n)$，因为内存不连续，需要遍历到目标位置

## 进阶技巧

### Dummy Node 哑巴/虚拟节点

- 为什么需要dummy？
	- 使用dummy node之后就不需要对头节点做特殊处理了
	- 当头节点不固定的时候(e.g. 可能会删除/交换当前头节点)就可以使用dummy node
- 凡是**需要对头节点做特殊操作**的时候，就可以使用dummy node
- 比如删除操作的时候需要找到目标节点的前一个节点，那么如果目标节点是头节点就需要特殊操作，所以我们再创建一个虚拟头节点`dummy = ListNode()` `dummy.next = head`，这样后面所有的节点都可以按照非头节点来处理，最好返回处理后的头节点`return dummy.next`

### 翻转链表

- 这里指in-place实现链表翻转，如果使用额外空间方法很多。
- 核心是改变每个node的next指向，需要从指向下一个节点变成指向前一个节点
- 假如我们当前遍历位置是c_node，前一个节点p_node，后一个n_node。我们需要**把c_node.next从指向n_node变成p_node**，如果直接`c_node.next = p_node`那么n_node将无法访问，也就不能继续遍历，所以在这之前需要暂存n_node
- 例题: [[1 P(Projects)/SDE Interview Prep/Algorithms/Leetcode/206 Reverse Linked List\|206 Reverse Linked List]]

```python
# store cur node and prev node during iteration
tmp = c_node.next
c_node.next = p_node
p_node = c_node
c_node = tmp # c_node = c_node.next
```

### 合并有序链表

- 三个指针l1、l2、p分别指向链表1、链表2、新合并的链表
- 使用dummy，dummy.next为新链表的头节点
- 每次比较l1.val和l2.val，p.next指向小的那个，对应l指针后移，p = p.next
- 如果链表1或链表2还有剩余元素，可以直接全部接到新链表的末尾
- 例题: [[1 P(Projects)/SDE Interview Prep/Algorithms/Leetcode/21 Merge Two Sorted Lists\|21 Merge Two Sorted Lists]], [[1 P(Projects)/SDE Interview Prep/Algorithms/Leetcode/23 Merge k Sorted Lists\|23 Merge k Sorted Lists]]

### 链表双指针 

- 链表的快慢指针也是[[1 P(Projects)/SDE Interview Prep/Algorithms/Topics/Two Pointers#快慢指针\|双指针-快慢指针]]中一个重要的组成部分 
- 例题:
	- [[1 P(Projects)/SDE Interview Prep/Algorithms/Leetcode/142 Linked List Cycle II\|142 Linked List Cycle II]] 环形链表经典问题
	- [[1 P(Projects)/SDE Interview Prep/Algorithms/Leetcode/160 Intersections of Two Linked Lists\|160 Intersections of Two Linked Lists]] 不算快慢指针但是也是链表双指针问题
	- [[1 P(Projects)/SDE Interview Prep/Algorithms/Leetcode/19 Remove Nth Node From End of List\|19 Remove Nth Node From End of List]]
