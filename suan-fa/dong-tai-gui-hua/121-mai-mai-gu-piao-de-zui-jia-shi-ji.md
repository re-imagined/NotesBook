# 121 买卖股票的最佳时机

{% tabs %}
{% tab title="普通遍历" %}
```java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length == 0) {
            return 0;
        }
        int maxProfit = 0;
        int min = prices[0];

        for (int i : prices) {
            if(i < min) { //  找最小值
                min = i;
            } else if (i - min > maxProfit) {  // 用当前值减最小值, 不断覆盖最大利润
                maxProfit = i - min; 
            }
        }
        return maxProfit;
    }
}
```
{% endtab %}

{% tab title="DP" %}
```java
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if len(prices) == 0:
            return 0
        res = 0
        dp = [[0 for i in range(3)] for j in range(len(prices))]

        # 维度i表示第i天
        # 维度j: 0 没有买过 1 已持有 2 之前持有且卖出
        # dp[i][j]表示的i天采取操作j的利润
        dp[0][0] = 0
        dp[0][1] = -prices[0]
        dp[0][2] = 0

        for i in range(1, len(prices)):
            # 前一天没有，今天也没有
            dp[i][0] = dp[i-1][0]  
            
            # 前一天买入 或 前一天已有
            dp[i][1] = max(dp[i-1][0] - prices[i], dp[i-1][1])  
            
            dp[i][2] = dp[i-1][1] + prices[i]
            
            res = max(dp[i][0], dp[i][1], dp[i][2], res)
        return res
```
{% endtab %}
{% endtabs %}

