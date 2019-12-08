# 49 全排列

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



