---
description: 非递归遍历树
---

# 94 二叉树的中序遍历



{% tabs %}
{% tab title="非递归" %}
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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> ret = new ArrayList<>();

        Stack<TreeNode> stack = new Stack<>();
        while(root != null || !stack.isEmpty()) {
            if (root != null) {
                stack.add(root);
                root = root.left;
            } else {
                root = stack.pop();
                ret.add(root.val);
                root = root.right;
            }
       
        }
        return ret;
    }
}
```
{% endtab %}

{% tab title="递归" %}
```java
class Solution {
    public List < Integer > inorderTraversal(TreeNode root) {
        List < Integer > res = new ArrayList < > ();
        helper(root, res);
        return res;
    }

    public void helper(TreeNode root, List < Integer > res) {
        if (root != null) {
            if (root.left != null) {
                helper(root.left, res);
            }
            res.add(root.val);
            if (root.right != null) {
                helper(root.right, res);
            }
        }
    }
}
```
{% endtab %}
{% endtabs %}

