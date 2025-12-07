# 42. Trapping Rain Water

**刷题日期**: 2025-12-06

**难度**: Hard

**标签**: Array, Two Pointers, Stack, Monotonic Stack

## 题目截图

![42. Trapping Rain Water](42_Trapping_Rain_Water.png)

## 代码

```java
class Solution {
    public int trap(int[] height) {
        Stack<Integer> stack = new Stack<>();
        int water = 0;

        for (int i = 0; i < height.length; i++) {
            while (!stack.isEmpty() && height[i] > height[stack.peek()]) {
                int mid = stack.pop();
                if (stack.isEmpty()) break;
                int leftIndex = stack.peek(), left = height[leftIndex];
                int wide = i - leftIndex - 1, h = Math.min(height[i], left) - height[mid];
                water += wide * h;
            }
            stack.push(i);
        }

        return water;
    }
}
```

## 复杂度分析

- **时间复杂度**: O(n) - 每个元素最多入栈出栈一次
- **空间复杂度**: O(n) - 栈最多存储 n 个元素

---
