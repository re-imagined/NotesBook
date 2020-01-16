# 279 完全平方数

给定正整数 _n_，找到若干个完全平方数（比如 `1, 4, 9, 16, ...`）使得它们的和等于 _n_。你需要让组成和的完全平方数的个数最少。

```text
输入: n = 12
输出: 3 
解释: 12 = 4 + 4 + 4.

输入: n = 13
输出: 2
解释: 13 = 4 + 9.
```

{% tabs %}
{% tab title="BFS" %}
```java
时间复杂度 O(n ∗ sqr(n))
空间复杂度 n

class Solution {
    class Node {
        int val;
        int step;
        public Node (int val, int step) {
            this.val = val;
            this.step = step;
        }
    }
    public int numSquares(int n) {
        Queue<Node> queue = new LinkedList<>();
        queue.add(new Node(n, 1));
        boolean[] record = new boolean[n];
        
        while (!queue.isEmpty()) {
            Node cur = queue.poll();
            for (int i = 1;; i++) {
                int nextVal = cur.val - i * i;
                if (nextVal < 0) {
                    break;
                } 
                if (nextVal == 0) {
                    return cur.step;
                }
                // 当再次出现时没有必要加入，因为在该节点的路径长度肯定不小于第一次出现的路径长
                if (!record[nextVal]) {
                    queue.add(new Node(nextVal, cur.step + 1));
                    record[nextVal] = true;
                }
            }
        }
        return -1;
    }
}
```
{% endtab %}

{% tab title="DP" %}
```java
时间复杂度O(n*sqrt(n))

class Solution {

    public int numSquares(int n) {
        int[] dp = new int[n+1];
        for (int i = 1; i <= n; i ++) {
            dp[i] = i;
            for (int j = 1; j * j <= i; j++) {
                dp[i] = Math.min(dp[i], dp[i - j * j] + 1);
            }
        }
        return dp[n];
    }
}
```
{% endtab %}
{% endtabs %}

