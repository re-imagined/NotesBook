---
description: BFS
---

# 429 N叉树的层序遍历

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
    public List<List<Integer>> levelOrder(Node root) {
        List<List<Integer>> res = new ArrayList<>();

        if (root == null ){
            return res;
        }
        LinkedList<Node> q = new LinkedList<>();
        q.add(root);
        while (!q.isEmpty()) {
            int s = q.size();
            List<Integer> cur = new ArrayList<>();
            for (int i = 0; i < s; i ++) {
                Node n = q.poll();
                cur.add(n.val);
                for (Node c : n.children) {
                    q.add(c);
                }
            }
            res.add(cur);
        }
        return res;
    }
}
```

