---
description: 输入不重复
---

# 46 全排列

给定一个没有重复数字的序列，返回其所有可能的全排列。

```text
示例:
输入: [1,2,3]
输出: [ [1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], [3,2,1]]
```

题解：

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        LinkedList<Integer> cur = new LinkedList<>();
        List<List<Integer>> ans = new ArrayList<>();
        int[] used = new int[nums.length];
        dfs(nums, used, new ArrayList<Integer>(), ans);
        return ans;
        
    }

    private void dfs(int[] nums, int[] used, ArrayList<Integer> cur, 
            List<List<Integer>> ans) {
        
        if (cur.size() == nums.length) {
            ans.add(new ArrayList<Integer>(cur));
            return;
        }
        for (int i = 0; i < nums.length; i++) {
            if (used[i] == 1) {
                continue;
            }
            used[i] = 1;
            cur.add(nums[i]);
            dfs(nums, used, cur, ans);
            cur.remove(cur.size() - 1);
            used[i] = 0;
        }
    }
}
```

![&#x56FE;&#x7247;&#x8F6C;&#x81EA;leetcode](../../../.gitbook/assets/image%20%286%29.png)

