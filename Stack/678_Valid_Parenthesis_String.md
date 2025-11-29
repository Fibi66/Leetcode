# 678. Valid Parenthesis String

**刷题日期**: 2025-11-28

**难度**: Medium

**标签**: Stack, String, Greedy

## 题目截图

![678_Valid_Parenthesis_String](678_Valid_Parenthesis_String.png)

## 解题心得

- 核心思路是用 Stack 来匹配索引
- 使用两个栈分别存储 `(` 和 `*` 的索引
- 遇到 `)` 时优先用 `(` 匹配，再用 `*` 匹配
- 最后用剩余的 `*` 匹配剩余的 `(`，注意 `(` 必须在 `*` 前面才能匹配
- 也可以不用双栈，单栈的做法是用两个 counter（`minOpen` 和 `maxOpen`）来记录未匹配左括号的可能范围，遇到 `(` 两者都加 1，遇到 `)` 两者都减 1，遇到 `*` 则 `minOpen` 减 1、`maxOpen` 加 1，最后检查 `minOpen == 0` 即可

## 代码

```java
class Solution {
    public boolean checkValidString(String s) {
        Stack<Integer> leftStack = new Stack<>();  // 存'('的索引
        Stack<Integer> starStack = new Stack<>();  // 存'*'的索引

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == '(') {
                leftStack.push(i);
            } else if (c == '*') {
                starStack.push(i);
            } else { // c == ')'
                if (!leftStack.isEmpty()) {
                    leftStack.pop();  // 优先用'('匹配
                } else if (!starStack.isEmpty()) {
                    starStack.pop();  // 再用'*'匹配
                } else {
                    return false;  // 没有可匹配的
                }
            }
        }

        // 用剩余的'*'匹配剩余的'('
        while (!leftStack.isEmpty() && !starStack.isEmpty()) {
            if (leftStack.pop() > starStack.pop()) {
                return false;  // '('在'*'后面，无法匹配
            }
        }

        return leftStack.isEmpty();
    }
}
```

## 复杂度分析

- **时间复杂度**: O(n) - 遍历字符串一次
- **空间复杂度**: O(n) - 两个栈最坏情况下存储所有字符的索引

---
