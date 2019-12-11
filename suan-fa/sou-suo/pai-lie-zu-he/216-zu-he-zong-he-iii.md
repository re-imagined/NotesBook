# 216 组合总和 III

找出所有相加之和为 n 的 k 个数的组合。

组合中只允许含有 1 - 9 的正整数，并且每种组合中不存在重复的数字。

此题与 [77 组合](77-zu-he.md) 几乎相同

说明：

* 所有数字都是正整数。 
* 解集不能包含重复的组合。

```java
class Solution {
    List<List<Integer>> ans = new LinkedList();
    int n;
    int k;
    public List<List<Integer>> combinationSum3(int k, int n) {
        this.n = n;
        this.k = k;
        dfs(1, n, new LinkedList<>());
        return ans;
    }

    private void dfs(int start, int target, LinkedList<Integer> cur) {
        if (cur.size() == k && target == 0) {
            ans.add(new LinkedList<>(cur));
        }
        for (int i = start; i < 10; ++i) {
            if (i > target) return;
            cur.add(i);
            dfs(i + 1, target - i, cur);
            cur.removeLast();
        }
    }
}
```

