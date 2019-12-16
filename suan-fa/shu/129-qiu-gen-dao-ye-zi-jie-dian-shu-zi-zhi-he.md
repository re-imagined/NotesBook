# 129 求根到叶子节点数字之和

```text
输入: [1,2,3]
    1
   / \
  2   3
输出: 25
解释:
从根到叶子节点路径 1->2 代表数字 12.
从根到叶子节点路径 1->3 代表数字 13.
因此，数字总和 = 12 + 13 = 25.


输入: [4,9,0,5,1]
    4
   / \
  9   0
 / \
5   1
输出: 1026
解释:
从根到叶子节点路径 4->9->5 代表数字 495.
从根到叶子节点路径 4->9->1 代表数字 491.
从根到叶子节点路径 4->0 代表数字 40.
因此，数字总和 = 495 + 491 + 40 = 1026.
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
    int res;
    public int sumNumbers(TreeNode root) {
        if (root == null) {
            return 0;
        }
        res = 0;
        dfs(root, 0);
        return res;

    }

    private void dfs(TreeNode root, int cur) {
        if (root == null) {
            return;
        }
        cur = cur * 10 + root.val;
        if (root.left == null && root.right == null) {
            res += cur;
            return;
        } 
        dfs(root.left, cur);
        dfs(root.right, cur);
    }
}
```

