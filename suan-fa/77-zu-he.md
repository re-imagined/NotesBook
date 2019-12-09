# 77 组合

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

