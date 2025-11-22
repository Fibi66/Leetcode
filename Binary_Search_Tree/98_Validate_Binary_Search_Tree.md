# 98. Validate Binary Search Tree

**刷题日期**: 2025-11-21

**难度**: Medium

**标签**: Tree, Depth-First Search, Binary Search Tree, Binary Tree

## 题目截图

![98. Validate Binary Search Tree - 1](98_Validate_Binary_Search_Tree_1.png)

![98. Validate Binary Search Tree - 2](98_Validate_Binary_Search_Tree_2.png)

![98. Validate Binary Search Tree - 3](98_Validate_Binary_Search_Tree_3.png)

## 解题心得

一开始是这样写的，但是这样只能检查单个 node，不能检查整棵树。意思是，如果一开始 root 是 5，那 5 的右边整棵树就不能有比 5 更小的。

然后就这样写了，还是错了。

最终正确解法：用 `Long.MIN_VALUE` 和 `Long.MAX_VALUE` 作为初始边界，递归时更新边界范围。

## 代码

```java
class Solution {
    public boolean isValidBST(TreeNode root) {
        return dfs(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    public boolean dfs(TreeNode root, long low, long high) {
        if (root == null) return true;
        if (root.val <= low || root.val >= high) return false;
        return dfs(root.left, low, root.val) && dfs(root.right, root.val, high);
    }
}
```

## 复杂度分析

- **时间复杂度**: O(n) - n 是二叉树的节点数，每个节点访问一次
- **空间复杂度**: O(h) - h 是树的高度，递归调用栈的深度，最坏情况下为 O(n)

---
