# 144 二叉树的前序遍历

给定一个二叉树，返回它的 _前序_ 遍历。

```text
示例:
输入: [1,null,2,3]  
   1
    \
     2
    /
   3 

输出: [1,2,3]
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
    public List<Integer> preorderTraversal(TreeNode root) {
        LinkedList<Integer> ret = new LinkedList<>();
        if (root == null) {
            return ret;
        }
        Stack<TreeNode> stack = new Stack<>();
        stack.add(root);

        while (!stack.isEmpty()) { // 栈pop顺序为 中-右-左, 是后续遍历的reverse
            TreeNode node = stack.pop();
            ret.add(node.val);
            if (node.right != null) stack.add(node.right);
            if (node.left != null) stack.add(node.left);
        }
        return ret;
    }
}
```

