# 234 回文链表

请判断一个链表是否为回文链表。

示例 1:

输入: 1-&gt;2 

输出: false 

示例 2:

输入: 1-&gt;2-&gt;2-&gt;1 

输出: true 

此题需要掌握快慢指针和停止时的节点状况

如果节点个数是奇数，慢指针最后会停在中间节点。

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
    public boolean isPalindrome(ListNode head) {
        if (head == null) return true;
        ListNode fast = head;
        ListNode slow = head;
        while (fast.next != null  && fast.next.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        // 反转中间节点的下一个节点之后的链表
        ListNode half1 = reverse(slow.next);
        ListNode half2 = head;
       
        // 偶数数节点时， fast会为null, head和pre正好是分成两个链表
        while (half1 != null && half2 != null) {
            if (half1.val != half2.val) {
                return false;
            }
            half1 = half1.next;
            half2 = half2.next;
        }
        return true;
    }

    private ListNode reverse(ListNode head) {
        ListNode pre = null;
        ListNode cur = pre;
        while (head != null) {
            cur = head.next;
            head.next = pre;
            pre = head;
            head = cur;
        }
        return pre;
    }
}
```



