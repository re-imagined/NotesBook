# 207 课程表

现在你总共有 n 门课需要选，记为 0 到 n-1。

在选修某些课程之前需要一些先修课程。 例如，想要学习课程 0 ，你需要先完成课程 1 ，我们用一个匹配来表示他们: \[0,1\]

给定课程总量以及它们的先决条件，判断是否可能完成所有课程的学习？

> 示例 1:
>
> 输入: 2, \[\[1,0\]\] 
>
> 输出: true 
>
> 解释: 总共有 2 门课程。学习课程 1 之前，你需要完成课程 0。所以这是可能的。

> 示例 2:
>
> 输入: 2, \[\[1,0\],\[0,1\]\] 
>
> 输出: false 
>
> 解释: 总共有 2 门课程。学习课程 1 之前，你需要先完成​课程 0；并且学习课程 0 之前，你还应先完成课程 1。这是不可能的。

说明:

输入的先决条件是由边缘列表表示的图形，而**不是邻接矩阵**。 详情请参见图的表示法。 你可以假定输入的先决条件中没有重复的边。

```java
class Solution {
    int[][] map;
    int[] visit;
    int len;

    public boolean canFinish(int numCourses, int[][] prerequisites) {
        len = numCourses;
        map = new int[len][len];
        
        // 构造n x n 的邻接矩阵
        for (int i = 0; i < prerequisites.length; i++ ) {
            map[prerequisites[i][1]][prerequisites[i][0]] = 1; 
        }
        visit = new int[len]; // 两个状态 visiting = 1, visited = 2

        for (int i = 0; i < len; i++) {
            if (!dfs(i)) return false;
        }
        return true;
    }

    private boolean dfs(int i) {
        if (visit[i] == 1) return false;
        if (visit[i] == 2) return true;
        visit[i] = 1;
        for(int j = 0; j < len; j++) {
            if (map[i][j] == 1 && !dfs(j))return false;
        }
        visit[i] = 2;
        return true;
    }
}
```

}

