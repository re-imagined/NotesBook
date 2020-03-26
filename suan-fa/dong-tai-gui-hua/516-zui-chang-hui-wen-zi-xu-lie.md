# 516 最长回文子序列

给定一个字符串s，找到其中最长的回文子序列。可以假设s的最大长度为1000。

示例 1:

 输入:"bbbab"

输出: 4 

一个可能的最长回文子序列为 "bbbb"。

示例 2: 

输入: "cbbd" 

输出:2 

一个可能的最长回文子序列为 "bb"。



解法参考

[https://docs.google.com/presentation/d/1KhxVVgI8jzc-g7unDNKFiHY6XDNVSK6LNsadxB14K3U/edit\#slide=id.g4dca2a952a\_1\_5](https://docs.google.com/presentation/d/1KhxVVgI8jzc-g7unDNKFiHY6XDNVSK6LNsadxB14K3U/edit#slide=id.g4dca2a952a_1_5)

```java
/**
 时间复杂度O(N^2), 空间复杂度O(N^2)
**/
class Solution {
    public int longestPalindromeSubseq(String s) {
        int n = s.length();
        int[][] dp = new int[n][n];

        for (int l = 1; l <= n; l++) {
            for (int i = 0; i <= n - l; i++) {
                int j = i + l - 1;
                if (i == j) {
                    dp[i][j] = 1;
                    continue;
                }
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = dp[i + 1][j - 1] + 2;
                } else {
                    dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
                }
            }
        }
        return dp[0][n - 1];
    }
}
```

