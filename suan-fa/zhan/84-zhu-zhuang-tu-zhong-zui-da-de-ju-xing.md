---
description: 单调栈 monotonic stack
---

# 84 柱状图中最大的矩形

给定 n 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。

求在该柱状图中，能够勾勒出来的矩形的最大面积。

![](../../.gitbook/assets/image%20%281%29.png)

以上是柱状图的示例，其中每个柱子的宽度为 1，给定的高度为 \[2,1,5,6,2,3\]。

![](../../.gitbook/assets/image%20%288%29.png)

图中阴影部分为所能勾勒出的最大矩形面积，其面积为 10 个单位。

{% tabs %}
{% tab title="O\(n\)" %}
```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int n = heights.length;
        int max = 0;
        Stack<Integer> stack = new Stack<>();
        stack.add(-1);

        for (int i = 0; i < n; i++) {
            while (stack.peek() != -1 && heights[stack.peek()] >= heights[i]) {
                max = Math.max(max, heights[stack.pop()] * (i - stack.peek() - 1));
            }
            stack.push(i);
        }
        while (stack.peek() != -1) {
            max = Math.max(max, heights[stack.pop()] * (n - stack.peek() - 1));
        }
        return max;
    }

}
```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="O\(nlogn\)" %}
```java
class Solution {
    public int largestRectangleArea3(int[] heights) {
        int maxArea = 0;
        for (int i = 0; i < heights.length; i ++) {
            int minHeight = Integer.MAX_VALUE;
            for (int j = i; j < heights.length; j++) {
                minHeight = Math.min(minHeight, heights[j]);
                maxArea = Math.max(maxArea, minHeight * (j - i + 1));
            }
        }
        return maxArea;
    }

    public int largestRectangleArea(int[] heights) {
        return getRectangleArea(heights, 0, heights.length - 1);
    }

    private int getRectangleArea(int[] heights, int start, int end) {
        if (start > end) {
            return 0;
        }
        int minHeightIdx = start;
        for (int i = start; i <= end; i ++) {
            if (heights[minHeightIdx] > heights[i]) {
                minHeightIdx = i;
            }
        }
        return Math.max(heights[minHeightIdx] * (end - start + 1), Math.max( 
                getRectangleArea(heights, start, minHeightIdx - 1), 
                getRectangleArea(heights, minHeightIdx + 1, end)));
    }
}
```
{% endtab %}
{% endtabs %}

