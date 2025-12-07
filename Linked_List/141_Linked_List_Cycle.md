# 141. Linked List Cycle

**刷题日期**: 2025-11-21, 2025-12-06

**复习次数**: 2

**难度**: Easy

**标签**: Hash Table, Linked List, Two Pointers

## 题目截图

![141. Linked List Cycle](141_Linked_List_Cycle.png)

## 解题心得

while 条件最应该注意：`fast != null && fast.next != null`

## 代码

```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) return false;

        ListNode slow = head, fast = head.next;
        while (fast != null && fast.next != null) {
            // while条件最应该注意
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) return true;
        }
        return false;
    }
}
```

## 复杂度分析

- **时间复杂度**: O(n) - n 是链表的长度，快慢指针最多遍历整个链表
- **空间复杂度**: O(1) - 只使用了两个指针变量

---
