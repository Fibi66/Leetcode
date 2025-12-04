# 56. Merge Intervals

**刷题日期**: 2025-12-03

**难度**: Medium

**标签**: Array, Sorting

## 题目截图

![屏幕截图 2025-12-03 235835](../屏幕截图%202025-12-03%20235835.png)

## 解题心得

本题的关键思路：
1. **先排序**：按照区间的起始位置排序，lambda表达式 `(a,b) -> a[0] - b[0]` 需要记住
2. **逐个合并**：遍历排序后的区间，每次与结果数组的最后一个区间比较
3. **判断重叠**：使用 `intervals[i][0] <= prev[1]` 判断是否重叠（注意是 `<=` 而不是 `<`）
4. **更新区间**：如果重叠，更新最后一个区间的结束位置为 `Math.max(prev[1], intervals[i][1])`
5. **List转数组**：`res.toArray(new int[res.size()][])` 是将List转为二维数组的标准写法，必须传入一个new object

## 代码

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals,
            (a,b) -> a[0] - b[0]  // 这个背一下
        );

        List<int[]> res = new ArrayList<>();
        res.add(intervals[0]);

        for (int i = 1; i < intervals.length; i++) {
            int[] prev = res.get(res.size() - 1);  //这里取的是res数组里的最后一位比较
            if (intervals[i][0] <= prev[1]) {  // <= 注意一下
                prev[1] = Math.max(prev[1], intervals[i][1]);
            } else {
                res.add(intervals[i]);
            }
        }

        return res.toArray(new int[res.size()][]);
        // 这个toArray必须用<T> T[] toArray(T[] a)才能转化二维array，就是必须传new object进
    }
}
```

## 复杂度分析

- **时间复杂度**: O(n log n)，主要消耗在排序上，遍历合并的时间复杂度为 O(n)
- **空间复杂度**: O(n)，需要额外的List来存储合并后的区间，最坏情况下所有区间都不重叠

---
