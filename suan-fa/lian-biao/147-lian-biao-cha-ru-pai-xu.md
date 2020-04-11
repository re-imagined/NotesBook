# 147 链表插入排序

插入排序的动画演示如上。从第一个元素开始，该链表可以被认为已经部分排序（用黑色表示）。 每次迭代时，从输入数据中移除一个元素（用红色表示），并原地将其插入到已排好序的链表中。

插入排序算法：

插入排序是迭代的，每次只移动一个元素，直到所有元素可以形成一个有序的输出列表。 每次迭代中，插入排序只从输入数据中移除一个待排序的元素，找到它在序列中适当的位置，并将其插入。 重复直到所有输入数据插入完为止。

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
    public ListNode insertionSortList(ListNode head) {
        if (head == null) return head;
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode pre = dummy;
        ListNode cur = head;
        ListNode tmp = null; 
        while (cur != null && cur.next != null) {
            if (cur.val <= cur.next.val) {
                cur = cur.next;
            } else {
                tmp = cur.next;
                cur.next = cur.next.next;
                pre = dummy;
                while (pre.next != null && pre.next.val < tmp.val) {
                    pre = pre.next;
                }
                tmp.next = pre.next;
                pre.next = tmp;
            }
        }
        return dummy.next;
    }
}
```

