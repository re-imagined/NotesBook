---
description: '非递归遍历树, BFS'
---

# 199 二叉树右视图

```text
输入: [1,2,3,null,5,null,4]
输出: [1, 3, 4]
解释:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---

```

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
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> res = new ArrayList<>();

        if (root == null) {
            return res;
        }
        LinkedList<TreeNode> q = new LinkedList<>();

        q.add(root);

        while (!q.isEmpty()) {
            int s = q.size();
            List<Integer> cur = new ArrayList<>();
            for (int i = 0; i < s; i ++ ) {
                TreeNode node = q.poll();
                if (i == s - 1) {
                    res.add(node.val);
                }
                if (node.left != null) {
                    q.add(node.left);
                }
                if (node.right != null) {
                    q.add(node.right);
                }
            }
        }
        return res;
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
    def rightSideView(self, root: TreeNode) -> List[int]:
        res = []
        self.recursion(root, 0, res);
        return res

    def recursion(self, root: TreeNode, level: int, res: List[int]):
        if not root:
            return
        if len(res) == level:
            res.append(root.val)
        self.recursion(root.right, level + 1, res)
        self.recursion(root.left, level + 1, res)
```
{% endtab %}
{% endtabs %}

