# 191 二进制中1的个数

时间复杂度：O\(1\) 。运行时间与 n 中位为 1的有关。在最坏情况下， n中所有位都是 1 。对于 32 位整数，运行时间是 O\(1\) 的。

空间复杂度：O\(1\)。没有使用额外空间。

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight2(int n) {
        int count = 0;
        while (n != 0) {
            count += n & 1;
            n >>>= 1;
        }
        return count;
    }

    public int hammingWeight(int n) {
        int count = 0;
        while (n != 0) {
            count ++;
            n = n & (n - 1);
        }
        return count;
    }
}
```

