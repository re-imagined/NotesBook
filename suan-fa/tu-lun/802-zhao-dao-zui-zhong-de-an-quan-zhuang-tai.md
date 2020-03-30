# 802 找到最终的安全状态

在有向图中, 我们从某个节点和每个转向处开始, 沿着图的有向边走。 如果我们到达的节点是终点 \(即它没有连出的有向边\), 我们停止。

现在, 如果我们最后能走到终点，那么我们的起始节点是最终安全的。 更具体地说, 存在一个自然数 K, 无论选择从哪里开始行走, 我们走了不到 K 步后必能停止在一个终点。

哪些节点最终是安全的？ 结果返回一个有序的数组。

该有向图有 N 个节点，标签为 0, 1, ..., N-1, 其中 N 是 graph 的节点数. 图以以下的形式给出: graph\[i\] 是节点 j 的一个列表，满足 \(i, j\) 是图的一条有向边。

> 示例： 
>
> 输入：graph = \[\[1,2\],\[2,3\],\[5\],\[0\],\[5\],\[\],\[\]\] 
>
> 输出：\[2,4,5,6\]

![](../../.gitbook/assets/image%20%289%29.png)

其实就是找到不在任何环中的节点

```java
class Solution {
    int UNKNOWN = 0;
    int VISTING = 1;
    int SAFE = 2;
    int UNSAFE = 3;
    public List<Integer> eventualSafeNodes(int[][] graph) {
        int[] status = new int[graph.length];
        List<Integer> res = new ArrayList<>();
        for (int i = 0; i < graph.length; i++) {
            if (dfs(graph, i, status) == SAFE) {
                res.add(i);
            }
        }
        return res;
    }

    private int dfs(int[][] graph, int cur, int[] status) {
        if (status[cur] == VISTING) {
            return UNSAFE;
        }
        if (status[cur] != UNKNOWN) {
            return status[cur];
        }
        status[cur] = VISTING;
        for (int next : graph[cur]) {
            if (dfs(graph, next, status) == UNSAFE) {
                status[cur] = UNSAFE;
                return UNSAFE;
            }
        }
        status[cur] = SAFE;
        return SAFE;
    }
}
```

