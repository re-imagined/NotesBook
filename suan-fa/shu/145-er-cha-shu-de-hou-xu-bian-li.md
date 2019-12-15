---
description: 非递归遍历树
---

# 145 二叉树的后序遍历

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
 /*
 *  左 -> 右 -> 中
 */
import java.util.Collections;

class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        
        LinkedList<Integer> ret = new LinkedList<>();
        if (root == null) {
            return ret;
        }
        LinkedList<TreeNode> q = new LinkedList<>();
        q.add(root);

        while (!q.isEmpty()) { 
            TreeNode node = q.pollLast();
            ret.addFirst(node.val);
            if (node.left != null) {
                q.add(node.left);
            }
            if (node.right != null) {
                q.add(node.right);
            }
        }
        return ret;

    }
}
```
{% endtab %}

{% tab title="递归" %}
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def postorderTraversal(self, root: TreeNode) -> List[int]:
        if not root:
            return []
        res = []
        self.recursion(root, res)
        return res
    
    def recursion(self, root: TreeNode, res: List[int]):
        if root:
            if root.left:
                self.recursion(root.left, res);
            if root.right:
                self.recursion(root.right, res);
            res.append(root.val)
```
{% endtab %}
{% endtabs %}

