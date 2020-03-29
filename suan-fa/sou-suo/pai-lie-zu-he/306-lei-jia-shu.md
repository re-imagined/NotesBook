---
description: 搜索 剪枝
---

# 306 累加数

相似题目 [842 将数组拆分成斐波那契序列](https://leetcode-cn.com/problems/split-array-into-fibonacci-sequence/)

  
累加数是一个字符串，组成它的数字可以形成累加序列。

一个有效的累加序列必须至少包含 3 个数。除了最开始的两个数以外，字符串中的其他数都等于它之前两个数相加的和。

给定一个只包含数字 '0'-'9' 的字符串，编写一个算法来判断给定输入是否是累加数。

说明: 累加序列里的数不会以 0 开头，所以不会出现 1, 2, 03 或者 1, 02, 3 的情况。

示例 1:

```text
输入: "112358" 
输出: true 
解释: 累加序列为: 1, 1, 2, 3, 5, 8 。1 + 1 = 2, 1 + 2 = 3, 2 + 3 = 5, 3 + 5 = 8 
```

示例 2:

```text
输入: "199100199" 
输出: true 
解释: 累加序列为: 1, 99, 100, 199。1 + 99 = 100, 99 + 100 = 199
```

```java
class Solution {
    public boolean isAdditiveNumber(String num) {
        int n = num.length();
        if (n < 3) {
            return false;
        }
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int a1 = 0;
                int a2 = i;
                int b1 = i + 1;
                int b2 = j;
                for (; ;) {
                    if (num.charAt(a1) == '0' && a1 != a2) break;
                    if (num.charAt(b1) == '0' && b1 != b2) break;
                    String c = add(num, a1, a2, b1, b2);
                    int c1 = b2 + 1;
                    int c2 = c1 + c.length() - 1;
                    if (c2 >= num.length()) break;
                    if (!c.equals(num.substring(c1, c2 +1))) break;
                    if (c2 == num.length() - 1) return true;

                    a1 = b1;
                    a2 = b2;
                    b1 = c1;
                    b2 = c2;
                }
         
            }
        }
        return false;
    }

    private String add(String num, int a1, int a2, int b1, int b2) {
        int len = Math.max((a2 - a1 + 1), (b2 - b1 + 1)) + 1;
        int[] nums = new int[len];
        for (int i = a2, j = b2, index = 0; i >= a1 || j >= b1; i--, j--, index ++) {
            if (i >= a1) {
                nums[index] += num.charAt(i) - '0';
            }
            if (j >= b1) {
                nums[index] += num.charAt(j) - '0';
            }
            nums[index + 1] = nums[index] / 10;
            nums[index] %= 10;
        }
        if (nums[len - 1] == 0) len --;
        StringBuilder sb = new StringBuilder();
        for (int i = len - 1; i >= 0; i--) {
            sb.append(nums[i]);
        }
        return sb.toString();

    }
}
```



