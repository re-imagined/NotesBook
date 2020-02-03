---
description: 字典树
---

# 386 字典序排数

定一个整数 n, 返回从 1 到 n 的字典顺序。

例如，

给定 n =1 3，返回 \[1,10,11,12,13,2,3,4,5,6,7,8,9\] 。

请尽可能的优化算法的时间复杂度和空间复杂度。 输入的数据 n 小于等于 5,000,000。



```java
class Solution {
    public List<Integer> lexicalOrder(int n) {
        List<Integer> res = new ArrayList<>();
        for (int i = 1; i < 10; i++) {
            dfs(i, n, res);
        }
        return res;
    }

    private void dfs (int target, int n, List<Integer> res) {
        if (target > n) return;
        res.add(target);
        target *= 10;
        for (int j = 0; j < 10; j ++) {
            dfs(target + j, n, res);
        }
    }
}
```

