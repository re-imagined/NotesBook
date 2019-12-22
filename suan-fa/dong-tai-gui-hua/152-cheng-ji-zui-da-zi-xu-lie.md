# 152 乘积最大子序列

```java
class Solution {
    public int maxProduct(int[] nums) {
        if (nums.length == 0) {
            return 0;
        }
        int[][] dp = new int[nums.length][2];
        dp[0][0] = nums[0];
        dp[0][1] = nums[0];
        int res = dp[0][1];
        for (int i = 1; i < nums.length; i++) {
            // nums[i]是正数，取最大
            dp[i][1] = Math.max(Math.max(dp[i - 1][1] * nums[i], dp[i - 1][0] * nums[i]), nums[i]);
            // nums[i]是负数，取最小s
            dp[i][0] = Math.min(Math.min(dp[i - 1][1] * nums[i], dp[i - 1][0] * nums[i]), nums[i]);
            if (dp[i][1] > res) res = dp[i][1];
        }
        return res;
    }
}
```

