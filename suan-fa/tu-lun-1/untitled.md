# Untitled

有 N 个网络节点，标记为 1 到 N。

给定一个列表 times，表示信号经过有向边的传递时间。 times\[i\] = \(u, v, w\)，其中 u 是源节点，v 是目标节点， w 是一个信号从源节点传递到目标节点的时间。

现在，我们从某个节点 K 发出一个信号。需要多久才能使所有节点都收到信号？如果不能使所有节点收到信号，返回 -1。

示例

![](../../.gitbook/assets/image%20%281%29.png)



```text
输入：times = [[2,1,1],[2,3,1],[3,4,1]], N = 4, K = 2
输出：2
```



1. `N` 的范围在 `[1, 100]` 之间。
2. `K` 的范围在 `[1, N]` 之间。
3. `times` 的长度在 `[1, 6000]` 之间。
4.  所有的边 `times[i] = (u, v, w)` 都有 `1 <= u, v <= N` 且 `0 <= w <= 100`。

solution 1 - bellman ford 算法

```java
class Solution {
    int MAX = 101 * 100;
    public int networkDelayTime(int[][] times, int N, int K) {
        int[] dist = new int[N];
        Arrays.fill(dist, MAX);
        dist[K - 1] = 0;
        for (int i = 1; i < N; i ++) {
            for (int[] time : times) {
                int u = time[0] - 1; 
                int v = time[1] - 1;
                int w = time[2];
                dist[v] = Math.min(dist[v], dist[u] + w);
            }
        }
        int res = 0;
        for (int d : dist) {
            if (d == MAX) {
                return -1;
            } else {
                res = Math.max(res, d);
            }
        }
        return res;
    }
}
```





