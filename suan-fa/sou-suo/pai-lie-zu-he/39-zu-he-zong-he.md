---
description: 无限 重复 选取
---

# 39 组合总和

给定一个无重复元素的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的数字可以**无限制重复被选取**。

> 说明： 所有数字（包括 target）都是正整数。 解集不能包含重复的组合。

```text
示例 1:
输入: candidates = [2,3,6,7], target = 7,
所求解集为:
[
  [7],
  [2,2,3]
]

示例 2:
输入: candidates = [2,3,5], target = 8,
所求解集为:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```

```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(candidates);
        search(candidates, target, 0, new ArrayList<>(), ans);
        return ans;
    }
    
    private void search(int[] candidates, int target, int start, 
            ArrayList<Integer> cur, List<List<Integer>> ans){
        
        if (target == 0) {
            ans.add(new ArrayList<>(cur));
            return;
        }
        for (int i = start; i < candidates.length; i++) {
            if (candidates[i] > target) break;
            cur.add(candidates[i]);
            // 下一个开始的位置还是i，这是重复选取的关键
            search(candidates, target - candidates[i], i, cur, ans);
            cur.remove(cur.size() - 1);
        }
    }
}
```

