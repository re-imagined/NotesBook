# 373 查找和最小的K对数字

给定两个以升序排列的整形数组 nums1 和 nums2, 以及一个整数 k。

定义一对值 \(u,v\)，其中第一个元素来自 nums1，第二个元素来自 nums2。

找到和最小的 k 对数字 \(u1,v1\), \(u2,v2\) ... \(uk,vk\)。

示例 1:

`输入: nums1 = [1,7,11], nums2 = [2,4,6], k = 3`   
`输出: [1,2],[1,4],[1,6]   
解释: 返回序列中的前 3 对数： [1,2],[1,4],[1,6],[7,2],[7,4],[11,2],[7,6],[11,4],[11,6]`

```java
class Solution {
    public List<List<Integer>> kSmallestPairs(int[] nums1, int[] nums2, int k) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums1.length == 0 ||nums2.length == 0 || k <= 0) return res;
        PriorityQueue<List<Integer>> queque = new PriorityQueue<>((o1, o2) -> {
            int a = o1.get(1) + o1.get(0);
            int b = o2.get(1) + o2.get(0);
            return a - b;
        });
        for (int i = 0; i < nums1.length && i < k; i++) {
            queque.add(Arrays.asList(nums1[i], nums2[0], 0)); // 第三位是指在nums2中取第几个
        } 
        while (!queque.isEmpty() && k-- > 0) {
            List<Integer> cur = queque.poll();
            res.add(Arrays.asList(cur.get(0), cur.get(1)));
            if (cur.get(2) + 1 == nums2.length) {
                continue;
            }
            queque.add(Arrays.asList(cur.get(0), nums2[cur.get(2) + 1], cur.get(2) + 1));
        }
        return res;
    }
}
```

