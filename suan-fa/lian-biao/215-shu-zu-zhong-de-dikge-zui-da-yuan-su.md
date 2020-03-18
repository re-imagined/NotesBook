# 215 数组中的第K个最大元素

  
在未排序的数组中找到第 **k** 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

**示例 1:**

```text
输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
```

**示例 2:**

```text
输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
```

**说明:**

你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。

解法一：

使用大小为k的最小堆来实现

解法二：

使用快速排序的思想，假设对数组做一个从大到小的排序，以分界点为参考，如果分界点位置大于k，说明目标数字在前半段，此时只需对前半段做快排的partition即可。

时间复杂度 T\(n\) = T\(n\) + T\(n/2\) + T\(n/4\) + T\(n/8\)....., 所以是O\(n\) 

```java
class Solution {
    public int findKthLargest2(int[] nums, int k) {
        PriorityQueue<Integer> queue = new PriorityQueue<>((i1, i2) -> {
            return i1 - i2;
        });
        for (int n : nums) {
            queue.add(n);
            if (queue.size() > k) {
                queue.poll();
            }
        }
        return queue.peek();
    }

    public int findKthLargest(int[] nums, int k) {
        return findKthLargest(nums, 0, nums.length - 1, k-1);
    }

    private int findKthLargest(int[] nums, int start, int end, int k) {
        int p = partition(nums, start, end);
        if (p == k) {
            return nums[p];
        } else if (p < k) {
            return findKthLargest(nums, p + 1, end, k);
        } else {
            return findKthLargest(nums, start, p - 1, k);
        }
    }

    private int partition(int[] nums, int start, int end) {
        int p = nums[end];
        while (start < end) {
            while (start < end && nums[start] >= p ) {
                start++;
            }
            nums[end] = nums[start];

            while (start < end && nums[end] <= p) {
                end --;
            }
            nums[start] = nums[end];

        }
        nums[end] = p;
        return start;
    } 
}
```

