# 138 复制带随机指针的链表

给定一个链表，每个节点包含一个额外增加的随机指针，该指针可以指向链表中的任何节点或空节点。

要求返回这个链表的[**深拷贝**](https://baike.baidu.com/item/%E6%B7%B1%E6%8B%B7%E8%B4%9D/22785317?fr=aladdin)。 

![](../../.gitbook/assets/image%20%285%29.png)

```java
/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/
class Solution {
    public Node copyRandomList(Node head) {
        if (head == null) {
            return null;
        }
        HashMap<Node, Node> map = new HashMap<>();
        map.put(head, null);
        Node cur = head;
        while (cur != null) {
            Node copyNode = new Node(cur.val);
            map.put(cur, copyNode);
            
            if (cur.next != null && !map.containsKey(cur.next)) {
                map.put(cur.next, null);
            }
            cur = cur.next;
        
        }
        for (Node key : map.keySet()) {
            Node copyNode = map.get(key);
            copyNode.next = map.get(key.next);
            copyNode.random = map.get(key.random);
        }
        return map.get(head);
    }
}
```

