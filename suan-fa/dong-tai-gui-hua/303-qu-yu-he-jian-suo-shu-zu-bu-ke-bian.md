# 303 区域和检索 - 数组不可变

给定一个整数数组  _nums_，求出数组从索引 _i_ 到 _j_  \(_i_ ≤ _j_\) 范围内元素的总和，包含 _i,  j_ 两点。

**示例：**

```text
给定 nums = [-2, 0, 3, -5, 2, -1]，求和函数为 sumRange()

sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3
```

```java
class NumArray {
    int[] sum;
    public NumArray(int[] nums) {
        this.sum = new int[nums.length + 1];
        for (int i = 0; i < nums.length; i++) {
            sum[i + 1] = nums[i] + sum[i];
        }
    }
    
    public int sumRange(int i, int j) {
        return sum[j + 1] - sum[i];
    }
}

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * int param_1 = obj.sumRange(i,j);
 */
```

