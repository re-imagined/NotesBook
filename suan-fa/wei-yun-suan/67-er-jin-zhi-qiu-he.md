# 67 二进制求和

给定两个二进制字符串，返回他们的和（用二进制表示）。

输入为非空字符串且只包含数字 1 和 0。

示例 1:

输入: a = "11", b = "1" 输出: "100" 示例 2:

输入: a = "1010", b = "1011" 输出: "10101"

题目很简单，关键在于掌握从二进制加法和进位的规律

对于每一位，sum = \(bit1 + bit2 + carry\) % 2, 下一位进位 carry = sum / 2

```java
class Solution {
    public String addBinary(String a, String b) {
        int carry = 0;
        StringBuilder sb = new StringBuilder();
        for (int i = a.length() - 1, j = b.length() - 1; i >= 0 || j >= 0; i--, j--) {
            int sum = carry;
            sum += i >= 0 ? a.charAt(i) - '0' : 0;
            sum += j >= 0 ? b.charAt(j) - '0' : 0;
            sb.append(sum % 2);
            carry = sum / 2;
        }
        sb.append(carry == 1 ? '1' : "");
        return sb.reverse().toString();
    }
}
```

