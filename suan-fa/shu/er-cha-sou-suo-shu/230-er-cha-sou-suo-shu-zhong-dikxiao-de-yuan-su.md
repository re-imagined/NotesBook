# 230 二叉搜索树中第K小的元素

给定一个二叉搜索树，编写一个函数 kthSmallest 来查找其中第 k 个最小的元素。

说明： 你可以假设 k 总是有效的，1 ≤ k ≤ 二叉搜索树元素个数。

示例 1:

```text
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 1
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

同理 , 求二叉搜索树的第k大元素

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
    public int kthLargest(TreeNode root, int k) {
        Stack<TreeNode> stack = new Stack<>();
        int count = 0;
        while (root != null || !stack.isEmpty()) {
            while (root != null) {
                stack.add(root);
                root = root.right;
            }
            count ++;
            TreeNode cur = stack.pop();
            if (count == k) {
                return cur.val;
            }
            root = cur.left;
        }
        return -1;
    }
}
```

