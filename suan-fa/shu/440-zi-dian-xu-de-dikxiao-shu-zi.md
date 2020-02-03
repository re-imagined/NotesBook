# 440 字典序的第K小数字

给定整数 n 和 k，找到 1 到 n 中字典序第 k 小的数字。

注意：1 ≤ k ≤ n ≤ 109。

```text
输入: n: 13 k: 2
输出: 10
解释: 字典序的排列是 [1, 10, 11, 12, 13, 2, 3, 4, 5, 6, 7,
```

```java
class Solution {
 int depth = 0;
    int res = 0;
    public int findKthNumber(int n, int k) {
        int cur = 1;
        while (k > 1) {
            long gap = findGap(cur, cur + 1, n);
            if (k > gap) { // 超过了当前的前缀字典树
                k -= gap;
                cur += 1;
            } else { // 还在同一个字典树
                cur *= 10;
                k -= 1;
            }
        }
        return (int)cur;
    }

    private long findGap(long a, long b, long n) {
        long gap = 0;
        while (a <= n) {
            gap += Math.min(n + 1, b) - a;
            a *= 10;
            b *= 10;
        }
        return gap;
    }
}
```

