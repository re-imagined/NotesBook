---
description: 输出不重复 全排列
---

# 47 全排列 II（去重）

给定一个可包含重复数字的序列，返回所有**不重复**的全排列。

```text
示例:
输入: [1,1,2] 
输出: [  [1,1,2], [1,2,1], [2,1,1]  ]
```

题解：

```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        int[] used = new int[nums.length];
        Arrays.sort(nums);
        dfs(nums, 0,  used, new ArrayList<Integer>(), ans);
        return ans;

    }
    
    private void dfs(int[] nums, int depth , int[] used, ArrayList<Integer> cur, 
            List<List<Integer>> ans) {
        
        if (nums.length == depth) {
            ans.add(new ArrayList<>(cur));
            return;
        }
        for (int i = 0; i < nums.length; i++) {
            if (used[i] == 1) continue;
            // 有数字相同，且索引更靠前的分支(将要被使用)，放弃此分支
            if (i > 0 && nums[i] == nums[i-1] && used[i-1] == 0) continue;  
            used[i] = 1;
            cur.add(nums[i]);
            dfs(nums, depth + 1, used, cur, ans);
            cur.remove(cur.size() - 1);
            used[i] = 0;
        }
    }
}
```

\*\*\*\*

