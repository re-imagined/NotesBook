---
description: DFS
---

# 113 路径总和 II

给定一个二叉树和一个目标和，找到所有从根节点到叶子节点路径总和等于给定目标和的路径。

说明: 叶子节点是指没有子节点的节点。

示例: 给定如下二叉树，以及目标和 sum = 22，

```text
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1

返回
[
   [5,4,11,2],
   [5,8,4,5]
]
```



```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        dfs(root, sum, res, new ArrayList<>());
        return res;
    }

    private void dfs(TreeNode root, int sum, List<List<Integer>> res, List<Integer> cur) {
        if (root == null) {
            return;
        }
        cur.add(root.val);
        sum -= root.val;
        if (root.left == null && root.right == null && sum == 0) {
            res.add(new ArrayList<>(cur));
        }
        dfs(root.left, sum, res, cur );
        dfs(root.right, sum, res, cur );
        cur.remove(cur.size() - 1);
        sum += root.val;
    }
}
```

