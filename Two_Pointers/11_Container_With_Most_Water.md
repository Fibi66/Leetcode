# 11. Container With Most Water

**刷题日期**: 2025-12-06, 2026-02-22

**复习次数**: 2

**难度**: Medium

**标签**: Array, Two Pointers, Greedy

## 题目截图

![11. Container With Most Water](11_Container_With_Most_Water.png)

## 解题心得

- 贪心，每次只依赖两根柱子

## 代码

```java
class Solution {
    public int maxArea(int[] height) {
        // 贪心，每次只依赖两根柱子
        int l = 0, r = height.length - 1;
        int maxWater = 0;
        while (l < r) {
            maxWater = Math.max(Math.min(height[l], height[r]) * (r - l), maxWater);
            if (height[l] < height[r]) {
                l++;
            } else {
                r--;
            }
        }
        return maxWater;
    }
}
```

## 复杂度分析

- **时间复杂度**: O(n) - 双指针遍历一次数组
- **空间复杂度**: O(1) - 只使用了常数个变量

---
