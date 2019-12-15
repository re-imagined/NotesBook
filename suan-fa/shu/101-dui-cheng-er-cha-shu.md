# 101 对称二叉树



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
    public boolean isSymmetric(TreeNode root) {
        if (root == null) {
            return true;
        }
        return recursion(root, root);
    }

    private boolean recursion(TreeNode p, TreeNode q) {
        if (p == null && p == null) return true;
        if (p == null || q == null) return false;
        return (q.val == p.val) 
            && recursion(p.left, q.right) 
            && recursion(p.right, q.left);
    }
}
```

