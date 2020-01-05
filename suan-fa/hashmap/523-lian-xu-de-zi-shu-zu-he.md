# 523 连续的子数组和

给定一个包含非负数的数组和一个目标整数 k，编写一个函数来判断该数组是否含有连续的子数组，其大小至少为 2，总和为 k 的倍数，即总和为 n\*k，其中 n 也是一个整数。

```text
输入: [0,1]
输出: 2
说明: [0, 1] 是具有相同数量0和1的最长连续子数组。

输入: [0,1,0]
输出: 2
说明: [0, 1] (或 [1, 0]) 是具有相同数量0和1的最长连续子数组。
```

把数组中的0换成1，则可变成前缀和问题

```java
class Solution {
    public boolean checkSubarraySum(int[] nums, int k) {
       
        int sum = 0;
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, -1);
        for (int i = 0; i < nums.length; i ++) {
            sum += nums[i];
            if (k != 0) {
                sum = sum % k;
            }
            if (!map.containsKey(sum)) {
                map.put(sum, i);
            } else {
                if (i - map.get(sum) > 1) {
                    return true;
                }
            }
        }
        return false;
    }
}
```

