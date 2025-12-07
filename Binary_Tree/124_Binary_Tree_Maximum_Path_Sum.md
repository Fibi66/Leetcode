# 124. Binary Tree Maximum Path Sum

**刷题日期**: 2025-12-07

**难度**: Hard

**标签**: Tree, Depth-First Search, Dynamic Programming, Binary Tree

## 题目截图

![124. Binary Tree Maximum Path Sum](124_Binary_Tree_Maximum_Path_Sum.png)

## 解题心得

- 如果 left 或者 right 是负数，就不要那边
- `root.val + left + right` 包含了所有场景，因为负数已经是 0 了不会走
- 如果两边都是负数，只会返回 root.val 自己
- dfs 返回的是单边最大路径：`Math.max(root.val + left, root.val + right)`

## 代码

```java
class Solution {
    private int max;
    public int maxPathSum(TreeNode root) {
        this.max = Integer.MIN_VALUE;
        dfs(root);
        return max;
    }

    private int dfs(TreeNode root) {
        if (root == null) return 0;
        // 如果left 或者right是负数, 就不要那边
        int left = Math.max(dfs(root.left), 0);
        int right = Math.max(dfs(root.right), 0);
        // root.val + left + right 包含了所有场景, 因为负数已经是0了不会走
        max = Math.max(max, root.val + left + right);
        // 如果两边都是负数, 只会返回root.val自己
        return Math.max(root.val + left, root.val + right);
    }
}
```

## 复杂度分析

- **时间复杂度**: O(n) - n 是二叉树的节点数，每个节点访问一次
- **空间复杂度**: O(h) - h 是树的高度，递归调用栈的深度，最坏情况下为 O(n)

---
