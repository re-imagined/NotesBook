# 合并K个排序链表

合并 _k_ 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。

```text
输入:
[
  1->4->5,
  1->3->4,
  2->6
]
输出: 1->1->2->3->4->4->5->6
```

假设K个链表每个长度都是n

合并两个链表的复杂度是O\(n\)，用merge sort的方式两两合并K个链表，复杂度是O\(klogK\)，所以 总的时间复杂度是O\(nKlogK\)

也可以解释为，merge sort的递归树深度为O\(logK\)，每层递归都要遍历nK个节点，于是复杂度是O\(nKlogK\)

空间复杂度是递归深度 O\(logK\)

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
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) {
            return null;
        }
        return merge(lists, 0, lists.length - 1);
    }

    private ListNode merge(ListNode[] lists, int l, int r){
        if (l > r) return null;
        if (l == r) return lists[l];
        if (l == r - 1) return mergeTwo(lists[l], lists[r]);
        int m = (r + l) / 2;
        ListNode l1 = merge(lists, l, m);
        ListNode l2 = merge(lists, m + 1, r);
        return mergeTwo(l1, l2);
    }

    public ListNode mergeTwo(ListNode l1, ListNode l2) {
        ListNode pre = new ListNode(0);
        ListNode tmp = pre;
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                tmp.next = l1;
                l1 = l1.next;
            }
            else {
                tmp.next = l2;
                l2 = l2.next;
            }
            tmp = tmp.next;
        }
        if (l1 != null){
            tmp.next = l1;
        }
        if (l2 != null){
            tmp.next = l2;
        }
        return pre.next;
    }
}
```

