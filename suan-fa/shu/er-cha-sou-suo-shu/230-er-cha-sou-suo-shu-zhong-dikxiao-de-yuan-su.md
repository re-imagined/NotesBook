# 230 二叉搜索树中第K小的元素

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
    public int kthSmallest(TreeNode root, int k) {
        if (root == null) return 0;
        LinkedList<TreeNode> queue = new LinkedList<>();
        while (root != null || queue.size() > 0) {
            while (root != null) {
                queue.add(root);
                root = root.left;
            }
            root = queue.pollLast();
            if (--k == 0) {
                return root.val;
            }
            root = root.right;
        }
        return 0;
    }
}
```

