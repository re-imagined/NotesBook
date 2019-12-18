---
description: 子集去重
---

# 90 子集II

给定一个可能包含重复元素的整数数组 _**nums**_，返回该数组所有可能的子集（幂集）。

**说明：**解集不能包含重复的子集。

```java
输入: [1,2,2]
输出:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

```java
class Solution {
  
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(nums); // 排序后才能根据相邻排除重复
        dfs(nums, 0, new ArrayList<>(), res);
        return res;
    }

    public void dfs(int[] nums, int start, ArrayList<Integer> cur, 
            List<List<Integer>> res) {

        res.add(new ArrayList(cur));
     
        for (int i = start ; i < nums.length; i++) {
            if (i > start && nums[i] == nums[i - 1]) continue;
            cur.add(nums[i]);
            dfs(nums, i + 1, cur, res);
            cur.remove(cur.size() - 1);
        }
    }
}
```

