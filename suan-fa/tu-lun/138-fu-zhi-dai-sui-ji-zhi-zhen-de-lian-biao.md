# 138 复制带随机指针的链表

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

