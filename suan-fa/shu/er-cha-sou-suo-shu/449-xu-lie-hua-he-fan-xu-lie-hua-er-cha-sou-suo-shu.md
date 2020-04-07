# 449 序列化和反序列化二叉搜索树

序列化是将数据结构或对象转换为一系列位的过程，以便它可以存储在文件或内存缓冲区中，或通过网络连接链路传输，以便稍后在同一个或另一个计算机环境中重建。

设计一个算法来序列化和反序列化二叉搜索树。 对序列化/反序列化算法的工作方式没有限制。 您只需确保二叉搜索树可以序列化为字符串，并且可以将该字符串反序列化为最初的二叉搜索树。

编码的字符串应尽可能紧凑。

注意：不要使用类成员/全局/静态变量来存储状态。 你的序列化和反序列化算法应该是无状态的。

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
public class Codec {
    StringBuilder sb = new StringBuilder();
    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {

        if (root == null) return null;
        preOrder(root);
        if(sb.length() > 0){
            sb.deleteCharAt(sb.length() - 1);
        }
        return sb.toString();
    }

    private void preOrder(TreeNode root) {
        if (root == null) return;
        sb.append(root.val);
        sb.append(" ");
        preOrder(root.left);
        preOrder(root.right);
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if (data == null || data.length() == 0) return null;
        String[] split = data.split(" ");
        LinkedList<Integer> nums = new LinkedList<>();
        for (String s : split) {
            nums.add(Integer.valueOf(s));
        }
        TreeNode root = buildTree(nums, Integer.MIN_VALUE, Integer.MAX_VALUE);
        return root;
    }

    private TreeNode buildTree(LinkedList<Integer> nums, Integer min, Integer max) {
        if (0 == nums.size()) return null;
        int val = nums.getFirst();
        if (val < min || val > max) {
            return null;
        }
        nums.poll();
        TreeNode node = new TreeNode(val);
        
        node.left = buildTree(nums, min, val);
        node.right = buildTree(nums, val, max);
        return node;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```

