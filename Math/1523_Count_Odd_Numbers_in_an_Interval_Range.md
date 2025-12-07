# 1523. Count Odd Numbers in an Interval Range

**刷题日期**: 2025-12-06

**难度**: Easy

**标签**: Math

## 题目截图

![1523. Count Odd Numbers in an Interval Range](1523_Count_Odd_Numbers_in_an_Interval_Range.png)

## 解题心得

- 长度是奇数时，看起始点是奇还是偶

## 代码

```java
class Solution {
    public int countOdds(int low, int high) {
        int count = high - low + 1;
        if (count % 2 == 0) {
            return count / 2;
        } else {
            // 长度是奇数时, 看起始点是奇还是偶
            return low % 2 == 1 ? count/2 + 1 : count/2;
        }
    }
}
```

## 复杂度分析

- **时间复杂度**: O(1) - 只进行简单的数学运算
- **空间复杂度**: O(1) - 只使用了常数个变量

---
