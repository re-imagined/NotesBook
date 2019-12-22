# 300 最长上升子序列

{% tabs %}
{% tab title="DP" %}
```java
class Solution {
    // 动态规划，dp[i]表示到底i个元素为止的最长上升子序列
    public int lengthOfLIS(int[] nums) {
        if (nums.length == 0) return 0;
        int[] dp = new int[nums.length];

        int res = 1;
        for (int i = 0; i < nums.length; i++) {
            dp[i] = 1;
            for (int j = 0; j < i ; j++) {
                if (nums[i] > nums[j] && dp[i] < dp[j] + 1) {
                    dp[i] = dp[j] + 1;
                }
            }
            if (dp[i] > res) res = dp[i];
        }
        return res;
    }
}
```
{% endtab %}

{% tab title="二分查找" %}
```python
# 时间复杂度 O(nlogn)  其中logn是二分查找的复杂度
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        if len(nums) == 0:
            return 0
        lis = [nums[0]]
        l = len(nums)
        for i in range(l):
            low = self.lowerBound(lis, nums[i])
            if low == len(lis):
                lis.append(nums[i])
            else:
                lis[low] = nums[i]
        
        return len(lis)

    def lowerBound(self, array: List[int], value: int) -> int:
        low = 0
        high = len(array)
        while low < high:
            mid = int((low + high) / 2)
            if value <= array[mid]:
                high = mid
            else:
                low = mid + 1
        
        return low
```
{% endtab %}
{% endtabs %}

