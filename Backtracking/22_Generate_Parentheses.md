# 22. Generate Parentheses

**Date**: 2025-11-23, 2025-12-04, 2025-12-07

**Times Reviewed**: 3

**Difficulty**: Medium

**Tags**: String, Backtracking

## Problem Screenshot

![22. Generate Parentheses](22_Generate_Parentheses.png)

## Notes

- For backtracking, just keep two conditions: `open > 0` and `close > open`
- Remember the StringBuilder API to delete a character: `sb.deleteCharAt(sb.length() - 1)`

**2025-12-07 Review**:
- Remember this condition — it's close greater than open: `if (close > open)`

## Code
```java
class Solution {
    List<String> res = new ArrayList<>();
    int pair;

    public List<String> generateParenthesis(int n) {
        this.pair = n;
        backtracking(new StringBuilder(), n, n);
        return res;
    }

    public void backtracking(StringBuilder sb, int open, int close) {
        if (open == 0 && close == 0) {
            res.add(sb.toString());
        }

        if (open > 0) { // just need this condition
            sb.append('(');
            backtracking(sb, open - 1, close);
            sb.deleteCharAt(sb.length() - 1); // remember this API
        }

        if (close > open) { // just need this condition
            sb.append(')');
            backtracking(sb, open, close - 1);
            sb.deleteCharAt(sb.length() - 1);
        }
    }
}
```

## Complexity Analysis

- **Time Complexity**: O(4^n / √n) - asymptotic bound of the nth Catalan number
- **Space Complexity**: O(n) - recursion stack depth is 2n, StringBuilder max length is 2n

---