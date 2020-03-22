# 148 排序链表

在 _O_\(_n_ log _n_\) 时间复杂度和常数级空间复杂度下，对链表进行排序。  


```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    // 时间复杂度O(NlogN) 空间复杂度O(logN)
    public ListNode sortList2(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode slow = head;
        ListNode fast = head.next;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        ListNode mid = slow.next;
        slow.next = null;
        return merge(sortList(head), sortList(mid));
    }

    // 时间复杂度O(NlogN) 空间复杂度O(1)
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        int len = getListLength(head);
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode left;
        ListNode right;
        ListNode tail;
        for (int i = 1; i < len; i <<= 1) {
            ListNode pre = dummy;
            ListNode cur = pre.next;
            while (cur != null) {
                left = cur; // 第一段
                right = split(cur, i); // 第二段
                cur = split(right, i);  // 保存下一次的开头
                pre.next = merge(left, right); // 合并前两段, 并接到上一个循环的尾部
                while (pre.next != null) { // 指针移到前两段的最后一个
                    pre = pre.next;
                }
            }
        }
        return dummy.next;
    }

    // 把链表分割为前n个和剩下的部分，反馈第n+1个节点, 第n个节点的next = null
    private ListNode split(ListNode head, int n) {
        if (head == null) {
            return head;
        }
        int i = 1;
        while (i < n && head != null) {
            head = head.next;
            i++;
        }
        ListNode rest = head != null ? head.next : null;
        if (head != null) {
            head.next = null;
        }
        return rest;
    } 

    private int getListLength(ListNode head) {
        if (head == null) {
            return 0;
        }
        ListNode cur = head;
        int l = 1;
        while (cur != null) {
            cur = cur.next;
            l ++;
        }
        return l;
    }

    private ListNode merge(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(-1);
        ListNode pre = dummy;
        while (l1 != null && l2 != null) {
            if (l1.val > l2.val) {
                dummy.next = l2;
                dummy = dummy.next;
                l2 = l2.next; 
            } else{
                dummy.next = l1;
                dummy = dummy.next;
                l1 = l1.next;  
            }
       
        }
        if (l1 != null) {
            dummy.next = l1;
        }
        if (l2 != null) {
            dummy.next = l2;
        }
        return pre.next;
    }
}
```

