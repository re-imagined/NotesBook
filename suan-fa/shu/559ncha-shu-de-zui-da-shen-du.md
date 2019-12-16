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
        if(root == null) {
            return 0;
        }
        int res = 0;
        Stack<Node> stack = new Stack();
        stack.add(root);
        
        while (!stack.isEmpty()){
            int s = stack.size();
            for (int i = 0; i < s; i ++ ) {
                Node n = stack.pop();
                for (Node child : n.children) {
                    stack.add(child);
                }
            }
            res += 1;
        }
        return res;
    }
}
```
{% endtab %}
{% endtabs %}

