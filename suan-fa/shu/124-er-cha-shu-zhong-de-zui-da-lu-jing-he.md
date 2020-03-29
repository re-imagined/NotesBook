# 124 二叉树中的最大路径和

类似题目

LeetCode 687: Longest Univalue Path [https://www.youtube.com/watch?v=yX1hVhcHcH8](https://www.youtube.com/watch?v=yX1hVhcHcH8) 

LeetCode 543: Diameter of Binary Tree [https://www.youtube.com/watch?v=VuezJmuIyU4](https://www.youtube.com/watch?v=VuezJmuIyU4)



给定一个非空二叉树，返回其最大路径和。

本题中，路径被定义为一条从树中任意节点出发，达到任意节点的序列。该路径至少包含一个节点，且不一定经过根节点。

示例 1:

```text
输入: [1,2,3]
   1
  / \
 2   3
 
输出: 6 
```

示例 2:

```text
输入: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7
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
    private int res = Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root) {
        find(root);
        return res;
    }

    private int find(TreeNode root) {
        if (root == null) return 0;
        int l = Math.max(0, find(root.left));
        int r = Math.max(0, find(root.right));
        int sum = l + r + root.val;
        res = Math.max(sum, res);
        return Math.max(l, r) + root.val;
    }
}
```

