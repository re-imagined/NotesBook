# 389 找不同

给定两个字符串 _**s**_ 和 _**t**_，它们只包含小写字母。

字符串 _**t**_ 由字符串 _**s**_ 随机重排，然后在随机位置添加一个字母。

请找出在 _**t**_ 中被添加的字母。

**示例:**

```text
输入：
s = "abcd"
t = "abcde"

输出：
e

解释：
'e' 是那个被添加的字母。
```

```java
class Solution {
    public char findTheDifference(String s, String t) {
        char c = 0;
        for (char c1 : s.toCharArray()) {
            c ^= c1;
        }
        for (char c2 : t.toCharArray()) {
            c ^= c2;
        }
        return c;
    }
}
```

