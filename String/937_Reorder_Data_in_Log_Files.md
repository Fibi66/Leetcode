# 937. Reorder Data in Log Files

**刷题日期**: 2026-02-16

**难度**: Medium

**标签**: Array, String, Sorting

## 题目截图

![937. Reorder Data in Log Files](937_Reorder_Data_in_Log_Files.png)

## 解题心得

- 保持 digitList 顺序不变，只排序 letterList
- Step 1: 分组 — 通过判断第一个空格后的字符是否为数字来区分 digit-log 和 letter-log
- Step 2: 只排 letter log — 先按内容排序，内容相同则按标识符排序
- Step 3: 合并 — letterList 在前，digitList 在后

## 代码

```java
class Solution {
    public String[] reorderLogFiles(String[] logs) {
        List<String> digitList = new ArrayList<>();    // 保持顺序并执行
        List<String> letterList = new ArrayList<>();

        // Step 1: 分组
        for (String log : logs) {
            int firstSpace = log.indexOf(" ");
            char firstCharAfterSpace = log.charAt(firstSpace + 1);

            if (Character.isDigit(firstCharAfterSpace)) {
                digitList.add(log);
            } else {
                letterList.add(log);
            }
        }

        // Step 2: 只排 letter log
        letterList.sort((a, b) -> {
            String contentA = a.substring(a.indexOf(" ") + 1);
            String contentB = b.substring(b.indexOf(" ") + 1);

            int cmp = contentA.compareTo(contentB);
            if (cmp != 0) return cmp;
            return a.substring(0, a.indexOf(" ")).compareTo(b.substring(0, b.indexOf(" ")));
        });

        // Step 3: 合并
        List<String> result = new ArrayList<>(letterList);
        result.addAll(digitList);
        return result.toArray(new String[0]);
    }
}
```

## 复杂度分析

- **时间复杂度**: O(n * m * log n) - n 是日志数量，m 是日志最大长度，排序需要 O(n log n) 次比较，每次比较 O(m)
- **空间复杂度**: O(n * m) - 存储分组后的日志列表

---
