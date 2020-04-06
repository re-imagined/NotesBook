---
description: 非递归遍历树
---

# 589 N叉树前序遍历

给定一个 N 叉树，返回其节点值的_前序遍历_。

例如，给定一个 `3叉树` , 返回其前序遍历: `[1,3,5,6,2,4]`。

> #### 能否不用递归完成？

![](../../.gitbook/assets/image%20%284%29.png)

{% tabs %}
{% tab title="递归" %}
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
    public List<Integer> preorder(Node root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        
        help(root, res);
        return res;
    }

    private void help(Node root, List<Integer> res) {
        if (root == null) {
            return;
        }
        res.add(root.val);
        for (Node child : root.children) {
            help(child, res);
        }

    }


}
```
{% endtab %}

{% tab title="非递归" %}
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
借助栈来完成
出入栈顺序: 
1. 根入栈
while 栈非空
2. 出栈一个节点
3. 该节点的子节点倒序入栈
4. 回到2
*/
class Solution {
    public List<Integer> preorder(Node root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        Stack<Node> s = new Stack<>();
        s.push(root);
        while (!s.isEmpty()){
            Node n = s.pop();
            res.add(n.val);
            if (n.children != null && n.children.size() != 0) {
                for (int i = n.children.size() - 1; i >= 0; i--) {
                    s.push(n.children.get(i));
                }
            }

        }
        return res;
    }


}
```
{% endtab %}
{% endtabs %}

