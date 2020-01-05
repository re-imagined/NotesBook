# 334 递增的三元子序列

给定一个未排序的数组，判断这个数组中是否存在长度为 3 的递增子序列。

数学表达式如下:

> 如果存在这样的 i, j, k, 且满足 0 ≤ i &lt; j &lt; k ≤ n-1， 使得 arr\[i\] &lt; arr\[j\] &lt; arr\[k\] ，
>
> 返回 true ;
>
>  否则返回 false 。

**说明:** 要求算法的时间复杂度为 O\(_n_\)，空间复杂度为 O\(_1_\) 。

```text
输入: [1,2,3,4,5]
输出: true

输入: [5,4,3,2,1]
输出: false
```

```java
class Solution {
    public boolean increasingTriplet(int[] nums) {
        if (nums.length < 3) {
            return false;
        }
        int min = Integer.MAX_VALUE;
        int second_min = Integer.MAX_VALUE;

        for (int n : nums) {
            if (n <= min) {
                min = n;
            } else if (n <= second_min) {
                second_min = n;
            } else {
                return true;
            }
        }
        return false;
    }
}
```

