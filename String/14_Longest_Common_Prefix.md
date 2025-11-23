# 14. Longest Common Prefix

**刷题日期**: 2025-11-23

**难度**: Easy

**标签**: String

## 题目截图

![14. Longest Common Prefix](14_Longest_Common_Prefix.png)

## 代码

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs.length == 1) return strs[0];
        String prefix = strs[0];
        for (int i = 1; i < strs.length; i++) {
            while (!strs[i].startsWith(prefix)) {
                prefix = prefix.substring(0, prefix.length() - 1);
            }
        }
        return prefix;
    }
}
```

## 复杂度分析

- **时间复杂度**: O(S) - S 是所有字符串中字符数量的总和，最坏情况需要比较所有字符
- **空间复杂度**: O(1) - 只使用了常数个变量

---
