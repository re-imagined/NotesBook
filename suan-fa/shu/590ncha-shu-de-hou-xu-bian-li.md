---
description: 非递归遍历树
---

# 590 N叉树的后序遍历

给定一个 N 叉树，返回其节点值的_后序遍历_。

例如，给定一个 `3叉树` 

返回其后序遍历: `[5,6,3,2,4,1]`.

![](../../.gitbook/assets/image%20%2811%29.png)

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/
class Solution {
    public List<Integer> postorder(Node root) {
        LinkedList<Integer> res = new LinkedList<>();
        if (root == null) {
            return res;
        }
        LinkedList<Node> q = new LinkedList<>();
        q.add(root);
        while (!q.isEmpty()){
            Node cur = q.pollLast();
            res.addFirst(cur.val);
            for (Node n : cur.children){
                q.add(n);
            }
        }
        return res;
    }
}
```

