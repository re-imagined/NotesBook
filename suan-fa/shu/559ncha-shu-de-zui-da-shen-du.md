# 559 N叉树的最大深度

{% tabs %}
{% tab title="DFS" %}
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
    public int maxDepth(Node root) {
        if(root == null) {
            return 0;
        } else if(root.children.isEmpty()) {
            return 1;
        } else {
            List<Integer> h = new ArrayList<>();
            for (Node n : root.children){
                h.add(maxDepth(n));
            }
            return Collections.max(h) + 1;
        }
    }
}
```
{% endtab %}

{% tab title="BFS" %}
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
    public int maxDepth(Node root) {
        if(root == null) return 0;
        if(root.children.size() == 0) return 1;

        int res = 0;
        LinkedList<Node> queue = new LinkedList<>();
        queue.add(root);
        
        while (!queue.isEmpty()){
            int s = queue.size();
            res += 1;
            while(s > 0) {
                Node n = queue.poll();
                if (n.children.size() > 0) {
                    queue.addAll(n.children);
                }
                s--;
            }
        }
        return res;
    }
}
```
{% endtab %}
{% endtabs %}

