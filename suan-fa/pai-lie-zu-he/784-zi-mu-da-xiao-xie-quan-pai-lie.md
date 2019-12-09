# 784 字母大小写全排列

给定一个字符串`S`，通过将字符串`S`中的每个字母转变大小写，我们可以获得一个新的字符串。返回所有可能得到的字符串集合。

示例: 

```text
输入: S = "a1b2"
输出: ["a1b2", "a1B2", "A1b2", "A1B2"]

输入: S = "3z4"
输出: ["3z4", "3Z4"]

输入: S = "12345"
输出: ["12345"]
```

```java
class Solution {
    public List<String> letterCasePermutation(String S) {
        List<String> res = new ArrayList<>();
        dfs(S.toCharArray(), 0, res);
        return res;
    }

    private void dfs(char[] S, int i, List<String> res) {
        if (i == S.length) {
            res.add(new String(S));
            return;
        }
        dfs(S, i+1, res);  // 第一个什么都不做，当做答案之一
        if (Character.isLetter(S[i])) {
            S[i] ^= (1 << 5);
            dfs(S, i+1, res);
            S[i] ^= (1 << 5);
        }
    }
}
```

