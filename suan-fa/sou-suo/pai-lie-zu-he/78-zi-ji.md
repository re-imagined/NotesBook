---
description: 返回该数组所有 可能的子集
---

# 78 子集

给定一组**不含重复元素**的整数数组 _nums_，返回该数组所有可能的子集（幂集）。

> **说明：**解集不能包含重复的子集。

> ```text
> 输入: nums = [1,2,3]
> 输出:
> [
>   [3],
>   [1],
>   [2],
>   [1,2,3],
>   [1,3],
>   [2,3],
>   [1,2],
>   []
> ]
> ```

题解

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(nums);
        for (int i = 0; i <= nums.length; i ++) {
            dfs(nums, 0, i, 0, new ArrayList<>(), res);
        }
        return res;

    }

    public void dfs(int[] candidates, int depth, int n, int start, 
            ArrayList<Integer> cur, List<List<Integer>> res) {
        
        if (depth == n) {
            res.add(new ArrayList(cur));
            return;
        }
        for (int i = start ; i < candidates.length; i++) {
            cur.add(candidates[i]);
            dfs(candidates, depth + 1, n, i + 1, cur, res);
            cur.remove(cur.size() - 1);
        }
    }
}
```

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(nums);
        dfs(nums, 0, new ArrayList<>(), res);
        return res;
    }

    public void dfs(int[] nums, int start, ArrayList<Integer> cur, 
            List<List<Integer>> res) {

        res.add(new ArrayList(cur));
     
        for (int i = start ; i < nums.length; i++) {
            cur.add(nums[i]);
            dfs(nums, i + 1, cur, res);
            cur.remove(cur.size() - 1);
        }
    }
}
```

