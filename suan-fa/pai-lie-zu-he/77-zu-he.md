# 77 组合

给定两个整数 _n_ 和 _k_，返回 1 ... _n_ 中所有可能的 _k_ 个数的组合。

```text
输入: n = 4, k = 2
输出:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

```java
class Solution {
    List<List<Integer>> ans = new LinkedList();
    int n;
    int k;
    public List<List<Integer>> combine(int n, int k) {
        this.n = n;
        this.k = k;
        dfs(1, new LinkedList<>());
        return ans;
    }

    private void dfs(int start, LinkedList<Integer> cur) {
        if (cur.size() == k) {
            ans.add(new LinkedList<>(cur));
        }
        for (int i = start; i < n + 1; ++i) {
            cur.add(i);
            dfs(i + 1, cur);
            cur.removeLast();
        }
    }
}
```

