# 1382 将二叉搜索树变平衡

给你一棵二叉搜索树，请你返回一棵 平衡后 的二叉搜索树，新生成的树应该与原来的树有着相同的节点值。

如果一棵二叉搜索树中，每个节点的两棵子树高度差不超过 1 ，我们就称这棵二叉搜索树是 平衡的 。

如果有多种构造方法，请你返回任意一种。

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 * 先用中序便利获取二叉树元素的排序结果，
 * 然后用108题的思路，将排序数组转换为平衡二叉搜索树
 */
class Solution {
    List<Integer> nums = new ArrayList<>();
    public TreeNode balanceBST(TreeNode root) {
        inorder(root);
        return build(nums, 0, nums.size() - 1);
    }

    private TreeNode build(List<Integer> nums, int l, int r) {
        if (l > r) return null;
        int mid = (r + l) / 2;
        TreeNode root = new TreeNode(nums.get(mid));
        root.left = build(nums, l, mid - 1);
        root.right = build(nums, mid + 1, r);
        return root;
    }

    private void inorder(TreeNode root) {
        if (root == null) return;
        inorder(root.left);
        nums.add(root.val);
        inorder(root.right);
    }
}
```

