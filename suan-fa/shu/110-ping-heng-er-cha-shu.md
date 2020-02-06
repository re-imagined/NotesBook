---
description: 树的深度
---

# 110 平衡二叉树



给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：

> 一个二叉树_每个节点_ 的左右两个子树的高度差的绝对值不超过1。

```text
示例 1:

给定二叉树 [3,9,20,null,null,15,7]
    3
   / \
  9  20
    /  \
   15   7
   
返回 true 。


示例 2:

给定二叉树 [1,2,2,3,3,null,null,4,4]

       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
返回 false 。
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
    private boolean isBalanced = true;
    public boolean isBalanced(TreeNode root) {
        if (root == null) {
            return true;
        }
        getHeight(root);
        return isBalanced;
    }
    private int getHeight(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int leftHeight = getHeight(root.left);
        int rightHeight = getHeight(root.right);
        if (Math.abs(leftHeight - rightHeight) > 1) {
            isBalanced = false;
            return -1;
        }
        return Math.max(rightHeight, leftHeight) + 1;

    }
}
```

