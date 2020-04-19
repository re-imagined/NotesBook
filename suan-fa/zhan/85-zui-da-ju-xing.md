# 85 最大矩形

相似题目：[84 柱状图中的最大矩形](84-zhu-zhuang-tu-zhong-zui-da-de-ju-xing.md)，[221 最大正方形](../dong-tai-gui-hua/221-zui-da-zheng-fang-xing.md)（动态规划）

给定一个仅包含 0 和 1 的二维二进制矩阵，找出只包含 1 的最大矩形，并返回其面积。

**示例:**

```text
输入:
[
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
输出: 6
```

```java
class Solution {
    public int maximalRectangle(char[][] matrix) {
        if (matrix == null || matrix.length == 0) {
            return 0;
        }
        int max = 0;
        int[] height = new int[matrix[0].length];
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                if (matrix[i][j] == '0') {
                    height[j] = 0;
                } else if (matrix[i][j] == '1') {
                    height[j] += 1;
                }
            }
            max = Math.max(max, getMaxRectangleArea(height));

        }
        return max;
    }

    private int getMaxRectangleArea(int[] height) {
        int n = height.length;
        int max = 0;
        Stack<Integer> stack = new Stack<>();
        stack.add(-1);
        for (int i = 0; i < n; i++) {
            while (stack.peek() != -1 && height[stack.peek()] >= height[i]) {
                max = Math.max(max, height[stack.pop()] * (i - stack.peek() - 1));
            }
            stack.add(i);
        }
        while (stack.peek() != -1) {
            max = Math.max(max, height[stack.pop()] * (n - stack.peek() - 1));
        }
        
        return max;
    }


}
```

