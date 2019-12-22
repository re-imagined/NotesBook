---
description: BFS
---

# 133 克隆图

给定无向[**连通**](https://baike.baidu.com/item/%E8%BF%9E%E9%80%9A%E5%9B%BE/6460995?fr=aladdin)图中一个节点的引用，返回该图的[**深拷贝**](https://baike.baidu.com/item/%E6%B7%B1%E6%8B%B7%E8%B4%9D/22785317?fr=aladdin)（克隆）。图中的每个节点都包含它的值 `val`（`Int`） 和其邻居的列表（`list[Node]`）。

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> neighbors;

    public Node() {}

    public Node(int _val,List<Node> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
};
*/
class Solution {
    public Node cloneGraph(Node node) {
        if (node == null) {
            return null;
        }
        LinkedList<Node> q = new LinkedList<>();
        q.add(node);
        Map<Node, Node> workMap = new HashMap<>();
        workMap.put(node, null);
        while (!q.isEmpty()) {
            Node cur = q.poll();
            Node copy = new Node(cur.val, new ArrayList<>());
            workMap.put(cur, copy);

            for (Node neighbor : cur.neighbors) {
                if (!workMap.containsKey(neighbor)) {
                    q.add(neighbor);
                    workMap.put(neighbor, null);
                }
            }
        }
        for (Node oneNode : workMap.keySet()) {
            Node copyNode = workMap.get(oneNode);
            for (Node neighbor : oneNode.neighbors) {
                copyNode.neighbors.add(workMap.get(neighbor));
            }
        }
        return workMap.get(node);
    }
}
```

