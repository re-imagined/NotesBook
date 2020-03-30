# 114 二叉树展开为链表

原理同 144 二叉树前序遍历的非递归版本

给定一个二叉树，原地将它展开为链表。

例如，给定二叉树

```text
    1
   / \
  2   5
 / \   \
3   4   6

返回:

1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```

{% tabs %}
{% tab title="递归" %}
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
    public void flatten2(TreeNode root) {
        dfs(root);
    }

    private TreeNode dfs(TreeNode root) {
        if (root == null) {
            return null;
        }
        TreeNode left = dfs(root.left);
        TreeNode right = dfs(root.right);
        if (left != null) {
            left.right = root.right;
            root.right = root.left;
            root.left = null;
        }
        if (right != null) return right;
        if (left != null) return left;
        return root;
    }


}
```
{% endtab %}

{% tab title="非递归栈" %}
```java
public void flatten(TreeNode root) {
    if (root == null) return;
    TreeNode dummy = new TreeNode(0);
    LinkedList<TreeNode> queue = new LinkedList<>();
    queue.add(root);
    TreeNode pre = dummy;
    while (!queue.isEmpty()) {
        TreeNode cur = queue.pollLast();
        if (cur == null) continue;
        pre.right = cur;
        pre.left = null;
        queue.add(cur.right);
        queue.add(cur.left);
        pre = pre.right;
    }
    pre.left = null;
}
```
{% endtab %}
{% endtabs %}

