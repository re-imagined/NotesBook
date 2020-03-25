# 4 寻找两个有序数组的中位数

  
给定两个大小为 m 和 n 的有序数组 `nums1` 和 `nums2`。

请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 O\(log\(m + n\)\)。

你可以假设 `nums1` 和 `nums2` 不会同时为空。

**示例 1:**

```text
nums1 = [1, 3]
nums2 = [2]

则中位数是 2.0
```

**示例 2:**

```text
nums1 = [1, 2]
nums2 = [3, 4]

则中位数是 (2 + 3)/2 = 2.5
```

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        if (nums1.length > nums2.length) return findMedianSortedArrays(nums2, nums1);

        int len1 = nums1.length;
        int len2 = nums2.length;
        int low = 0, high = len1;


        while (low <= high) {
            int partition1 = (low + high) / 2;
            int partition2 = (len1 + len2 + 1) / 2 - partition1;
            int maxLeft1 = partition1 == 0 ? Integer.MIN_VALUE : nums1[partition1 - 1];
            int minRight1 = partition1 == len1 ? Integer.MAX_VALUE : nums1[partition1];

            int maxLeft2 = partition2 == 0 ? Integer.MIN_VALUE : nums2[partition2 - 1];
            int minRight2 = partition2 == len2 ? Integer.MAX_VALUE : nums2[partition2];

            if (maxLeft1 <= minRight2 && maxLeft2 <= minRight1) {
                if ((len1 + len2) % 2 == 0) {
                    return ((double)Math.max(maxLeft1, maxLeft2) + Math.min(minRight1, minRight2)) / 2;
                } else {
                    return (double)Math.max(maxLeft1, maxLeft2);
                }
            } else {
                if (maxLeft1 > minRight2) {
                    high = partition1 - 1;
                } else {
                    low = partition1 + 1;
                }
            }
        }
        return -1;
    }
}
```

