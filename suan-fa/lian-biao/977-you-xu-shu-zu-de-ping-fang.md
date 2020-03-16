# 977 有序数组的平方

给定一个按非递减顺序排序的整数数组 A，返回每个数字的平方组成的新数组，要求也按非递减顺序排序。

示例 1：

输入：\[-4,-1,0,3,10\] 输出：\[0,1,9,16,100\] 示例 2：

输入：\[-7,-3,2,3,11\] 输出：\[4,9,9,49,121\]

> 提示：
>
> 1 &lt;= A.length &lt;= 10000
>
>  -10000 &lt;= A\[i\] &lt;= 10000 
>
> A 已按非递减顺序排序。

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int j = 0;
        while(j < nums.length - 1 && nums[j] < 0) {
            j += 1;
        }
        int i = j - 1;
        int c = 0;
        int[] ret = new int[nums.length];
        while (i >= 0 && j < nums.length) {
            if (nums[i] * nums[i] > nums[j] * nums[j]) {
                ret[c++] = nums[j] * nums[j];
                j++;
            } else {
                ret[c++] = nums[i] * nums[i];
                i--;
            }
        }
        while (i >= 0) {
            ret[c++] = nums[i] * nums[i];
            i--;
        }
        while (j < nums.length) {
            ret[c++] = nums[j] * nums[j];
            j++;
        }
        return ret;
    }
}
```

