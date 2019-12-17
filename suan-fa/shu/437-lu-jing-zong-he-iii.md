# 437 路径总和 III

给定一个二叉树，它的每个结点都存放着一个整数值。

找出路径和等于给定数值的路径总数。

路径不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。

二叉树不超过1000个节点，且节点数值范围是 \[-1000000,1000000\] 的整数。

```text
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

返回 3。和等于 8 的路径有:

1.  5 -> 3
2.  5 -> 2 -> 1
3.  -3 -> 11
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
    int res;
    public int pathSum(TreeNode root, int sum) {
        if (root == null) {
            return 0;
        }
        dfs(root, new ArrayList<>(), sum);
        return res;
    }

    private void dfs(TreeNode root, List<Integer> path, int sum) {
        if (root == null) {
            return;
        }
        path.add(root.val);
        int cur = 0;
        for (int i = path.size() - 1; i >= 0; i-- ) {
            cur += path.get(i);
            if (cur == sum) {
                res ++;
            }
        }
        dfs(root.left, path, sum);
        dfs(root.right, path, sum);
        path.remove(path.size() - 1);

    }
}
```

