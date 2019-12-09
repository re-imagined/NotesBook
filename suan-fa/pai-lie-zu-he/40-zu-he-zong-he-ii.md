---
description: 每个数只能使用一次
---

# 40 组合总和 II

给定一个数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的每个数字在每个组合中**只能使用一次**。

说明：

所有数字（包括目标数）都是正整数。 解集不能包含重复的组合。 

示例 1:

```text
输入: 
candidates = [10,1,2,7,6,1,5], 
target = 8, 
所求解集为: [ [1, 7], [1, 2, 5], [2, 6], [1, 1, 6] ] 
```

示例 2:

```text
输入:
candidates = [2,5,2,1,2],
target = 5, 
所求解集为: [ [1,2,2], [5] ]
```

题解：

时间复杂度 O\(2^n\)

空间复杂度 O\(kn\)，k是结果的长度

```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        // 排序很重要
        Arrays.sort(candidates);
        int[] used = new int[candidates.length];
        dfs(candidates, used, target, 0, new ArrayList<>(), res);
        return res;

    }

    public void dfs(int[] candidates, int[] used, int target, int start, 
            ArrayList<Integer> cur, List<List<Integer>> res) {
        
        if (target == 0) {
            res.add(new ArrayList(cur));
            return;
        }
        for (int i = start ; i < candidates.length; i++) {
            if (candidates[i] > target) return;
            // 略过同样的数字
            if (i > start && candidates[i] == candidates[i - 1] ) continue;
            cur.add(candidates[i]);
            used[i] = 1;
            dfs(candidates, used, target - candidates[i], i + 1, cur, res);
            cur.remove(cur.size() - 1);
            used[i] = 0;
        }
    }
}
```

