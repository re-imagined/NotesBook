# 560  和为K的子数组

给定一个整数数组和一个整数 k，你需要找到该数组中和为 k 的连续的子数组的个数。

```text
输入:nums = [1,1,1], k = 2 
输出: 2 , [1,1] 与 [1,1] 为两种不同的情况。 

输入:nums = [1,1,1], k = 2 
输出: 2 , [1,1] 与 [1,1] 为两种不同的情况。 
```

数组的长度为 \[1, 20,000\]。 数组中元素的范围是 \[-1000, 1000\] ，且整数 k 的范围是 \[-1e7, 1e7\]。

```text
class Solution {
    public int subarraySum(int[] nums, int k) {
        Map<Integer, Integer> memo = new HashMap<>();
        memo.put(0, 1);
        int ans = 0;
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            ans += memo.getOrDefault(sum - k, 0);
            memo.put(sum, memo.getOrDefault(sum, 0) + 1);
        }
        return ans;
    }
}
```

