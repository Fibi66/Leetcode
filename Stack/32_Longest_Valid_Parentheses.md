# 32. Longest Valid Parentheses

**刷题日期**: 2025-11-23

**难度**: Hard

**标签**: String, Stack, Dynamic Programming

## 题目截图

![32. Longest Valid Parentheses](32_Longest_Valid_Parentheses.png)

## 解题心得

- 用 stack 记录下标 index
- 当遇到一个不匹配的时候，把下标推入
- 再拿出下标，看看哪个长度最长

## 代码

```java
class Solution {
    public int longestValidParentheses(String s) {
        // 用stack记录下标index
        // 当遇到一个不匹配的时候，把下标推入
        // 再拿出下标，看看哪个长度最长

        int n = s.length();
        Stack<Integer> stack = new Stack<>();
        stack.push(-1);
        for (int i = 0; i < n; i++) {
            if (s.charAt(i) == ')' && stack.size() > 1 && s.charAt(stack.peek()) == '(') {
                stack.pop();
            } else {
                stack.push(i);
            }
        }

        int max = 0, i = n;
        while (!stack.isEmpty()) {
            max = Math.max(max, i - 1 - stack.peek());
            i = stack.pop();
        }
        return max;
    }
}
```

## 复杂度分析

- **时间复杂度**: O(n) - 遍历字符串一次，再遍历栈一次
- **空间复杂度**: O(n) - 栈最多存储 n 个下标

---
