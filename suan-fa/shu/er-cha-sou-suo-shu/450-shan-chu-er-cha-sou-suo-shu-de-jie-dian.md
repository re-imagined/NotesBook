# 450 删除二叉搜索树的节点

给定一个二叉搜索树的根节点 root 和一个值 key，删除二叉搜索树中的 key 对应的节点，并保证二叉搜索树的性质不变。返回二叉搜索树（有可能被更新）的根节点的引用。

一般来说，删除节点可分为两个步骤：

首先找到需要删除的节点； 如果找到了，删除它。 说明： 要求算法时间复杂度为 O\(h\)，h 为树的高度。

示例:

```text
root = [5,3,6,2,4,null,7]
key = 3

    5
   / \
  3   6
 / \   \
2   4   7

给定需要删除的节点值是 3，所以我们首先找到 3 这个节点，然后删除它。

一个正确的答案是 [5,4,6,2,null,null,7], 如下图所示。

    5
   / \
  4   6
 /     \
2       7

另一个正确答案是 [5,2,6,null,4,null,7]。

    5
   / \
  2   6
   \   \
    4   7
```

![](../../../.gitbook/assets/image%20%283%29.png)

如果a.val == key, 那么只需将父节点指向a的指针置空即可

如果a.val == key, 只有左或右子树，只需将其父节点指向这个子树即可

如果a.val == key, 有左和右子树，在a的右子树中找最小节点m，替换到a的位置（在a的子树中一直往左走即可找到最小值），然后再递归地删除节点m

![](../../../.gitbook/assets/image%20%2810%29.png)

![](../../../.gitbook/assets/image%20%2815%29.png)

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
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) return root;
        if (root.val > key) {
            root.left = deleteNode(root.left, key);
        } else if (root.val < key) {
            root.right = deleteNode(root.right, key);
        } else {
            if (root.left == null || root.right == null) {
                TreeNode node = root.left == null ? root.right : root.left;
                root.left = null;
                root.right = null;
                return node;
            } else {
                TreeNode min = root.right;
                while (min.left != null) {
                    min = min.left;
                }
                root.val = min.val;
                root.right = deleteNode(root.right, min.val);
            }
        }
        return root;

    }

  
}
```

