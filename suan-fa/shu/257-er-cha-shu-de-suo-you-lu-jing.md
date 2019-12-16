---
description: DFS
---

# 257 二叉树的所有路径

给定一个二叉树，返回所有从根节点到叶子节点的路径。

**说明:** 叶子节点是指没有子节点的节点。

```text
输入:

   1
 /   \
2     3
 \
  5

输出: ["1->2->5", "1->3"]

解释: 所有根节点到叶子节点的路径为: 1->2->5, 1->3
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
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res = new ArrayList<>();

        if (root == null) {
            return res;
        }
        dfs(root, res, new ArrayList<>());
        return res;

    } 

    private void dfs(TreeNode root, List<String> res, List<String> cur) {
        if (root == null) {
            return;
        }
        cur.add(String.valueOf(root.val));
        if (root.left == null && root.right == null) {
            StringBuilder oneRes = new StringBuilder();
            for(int i = 0; i < cur.size(); i++) {
                if (i != cur.size() - 1) {
                    oneRes.append(cur.get(i)).append("->");
                } else {
                    oneRes.append(cur.get(i));
                }
            }
            res.add(oneRes.toString());
        }

        dfs(root.left, res, cur);
        dfs(root.right, res, cur);
        cur.remove(cur.size() - 1);
    }

}
```

