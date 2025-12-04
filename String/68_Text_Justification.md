# 68. Text Justification

**刷题日期**: 2025-12-03

**难度**: Hard

**标签**: Array, String, Simulation

## 题目截图

![屏幕截图 2025-12-03 230837](../屏幕截图%202025-12-03%20230837.png)

## 解题心得

本题需要注意排版时的两种情况：
1. **普通行**：需要在单词之间均匀分配空格，如果空格无法均匀分配，则左边的间隙要比右边多
2. **最后一行**：需要左对齐，单词之间只用一个空格，末尾填充空格

关键技巧：
- 使用 `gaps = Math.max(line.size() - 1, 1)` 来计算间隙数（注意只有一个单词时的特殊情况）
- 计算基本空格数：`space = spaceLeft / gaps`
- 计算多余空格数：`spaceRemainder = spaceLeft % gaps`，这些空格要依次分配到左边的间隙中

## 代码

```java
class Solution {
    public List<String> fullJustify(String[] words, int maxWidth) {
        int n = words.length;
        List<String> res = new ArrayList<>();
        List<String> line = new ArrayList<>();

        int i = 0;
        int length = 0;

        while (i < n) {
            // 判断当前单词能否加入当前行
            if (line.isEmpty() || (length + line.size() + words[i].length()) <= maxWidth) {
                // 把当前 words[i] 放进行里
                line.add(words[i]);
                length += words[i].length();
                i++;
            } else {
                // 当前行已满，需要进行排版
                int spaceLeft = maxWidth - length;
                int gaps = Math.max(line.size() - 1, 1);  // 间隔数
                int space = spaceLeft / gaps;  // 基本空格数
                int spaceRemainder = spaceLeft % gaps;  // 多余的空格数

                StringBuilder sb = new StringBuilder();

                for (int j = 0; j < line.size(); j++) {
                    sb.append(line.get(j));

                    if (j < line.size() - 1 || line.size() == 1) {
                        // 添加空格
                        int spacesToAdd = space;
                        if (j < spaceRemainder) {
                            spacesToAdd++;
                        }
                        for (int k = 0; k < spacesToAdd; k++) {
                            sb.append(' ');
                        }
                    }
                }

                res.add(sb.toString());

                // 开始新的一行
                line.clear();
                length = 0;
            }
        }

        // 处理最后一行，左对齐
        StringBuilder last = new StringBuilder();
        for (int j = 0; j < line.size(); j++) {
            if (j > 0) last.append(' ');
            last.append(line.get(j));
        }
        while (last.length() < maxWidth) last.append(' ');
        res.add(last.toString());

        return res;
    }
}
```

## 复杂度分析

- **时间复杂度**: O(n * m)，其中 n 是单词数量，m 是每行的最大宽度。需要遍历所有单词，并且对每行进行空格填充操作
- **空间复杂度**: O(n * m)，需要存储结果列表，最坏情况下每个单词占一行

---
