# 215. Kth Largest Element in an Array

**刷题日期**: 2025-12-07

**难度**: Medium

**标签**: Array, Divide and Conquer, Sorting, Heap (Priority Queue), Quickselect

## 题目截图

![215. Kth Largest Element in an Array](215_Kth_Largest_Element_in_an_Array.png)

## 解题心得

- pq 会把最小的数字排到最上面（小顶堆）
- 如果我们只把大于 pq 里的数字放进去，top 即使我们要的 kth 大
- 维护一个大小为 k 的小顶堆，堆顶就是第 k 大的元素

## 代码

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        // pq会把最小的数字排到最上面
        // 如果我们只把大于pq里的数字放进去, top即使我们要的kth 大
        for (int x : nums) {
            if (pq.size() < k) pq.offer(x);
            else {
                if (x > pq.peek()) {
                    pq.poll();
                    pq.offer(x);
                }
            }
        }
        return pq.peek();
    }
}
```

## 复杂度分析

- **时间复杂度**: O(n log k) - 遍历数组，每次堆操作是 O(log k)
- **空间复杂度**: O(k) - 堆的大小为 k

---
