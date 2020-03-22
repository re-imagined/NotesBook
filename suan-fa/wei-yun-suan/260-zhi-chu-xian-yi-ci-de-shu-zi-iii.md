# 260 只出现一次的数字 III

给定一个整数数组 `nums`，其中恰好有两个元素只出现一次，其余所有元素均出现两次。 找出只出现一次的那两个元素。

先对所有数字进行异或操作，最终结果就是那两个元素异或的结果，这两个元素不相同，这两个元素的二进制位上，一定有至少一个位不相同，也就是说这个结果中一定有一个二进制位为1（异或不同得1，相同得0），通过找到这个位，通过比较数组中的元素该为上是1还是0，把这些元素分割为两部分，其中每部分的元素各自异或的结果就是每部分中的目标元素

```java
class Solution {
    public int[] singleNumber(int[] nums) {
        int num = 0;
        for (int n : nums) {
            num ^= n;
        }
        int mask = 1;
        while (true) {
            if ((num & 1) == 1) {
                break;
            }
            mask = mask << 1;
            num = num >> 1;
        }
        int a = 0, b = 0;
        for (int n : nums) {
            if ((mask & n) == 0) {
                a ^= n;
            } else {
                b ^= n;
            }
        }
        return new int[] {a, b};
    }
}
```

