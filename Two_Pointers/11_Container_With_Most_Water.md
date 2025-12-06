# 11. Container With Most Water

**刷题日期**: 2025-12-06

**难度**: Medium

**标签**: Array, Two Pointers, Greedy

## 题目截图

![11. Container With Most Water](11_Container_With_Most_Water.png)

## 代码

```java
class Solution {
    public int maxArea(int[] height) {
        int l = 0, r = height.length - 1;
        int max = 0;
        while (l < r) {
            max = Math.max(Math.min(height[l], height[r]) * (r - l), max);

            if (height[l] < height[r]) l++;
            else r--;
        }

        return max;
    }
}
```

## 复杂度分析

- **时间复杂度**: O(n) - 双指针遍历一次数组
- **空间复杂度**: O(1) - 只使用了常数个变量

---
