# 1254 统计封闭岛屿的数目

有一个二维矩阵 grid ，每个位置要么是陆地（记号为 0 ）要么是水域（记号为 1 ）。

我们从一块陆地出发，每次可以往上下左右 4 个方向相邻区域走，能走到的所有陆地区域，我们将其称为一座「岛屿」。

如果一座岛屿 完全 由水域包围，即陆地边缘上下左右所有相邻区域都是水域，那么我们将其称为 「封闭岛屿」。

请返回封闭岛屿的数目。

```text
输入：grid = 
    [[1,1,1,1,1,1,1,0],
     [1,0,0,0,0,1,1,0],
     [1,0,1,0,1,1,1,0],
     [1,0,0,0,0,1,0,1],
     [1,1,1,1,1,1,1,0]]
输出：2
解释：
灰色区域的岛屿是封闭岛屿，因为这座岛屿完全被水域包围（即被 1 区域包围）。
```



![](../../.gitbook/assets/image%20%284%29.png)

```java
class Solution {
    int valid;

    public int closedIsland(int[][] grid) {
        int len = grid.length;
        int width = grid[0].length;
        int res = 0;
        for (int i = 0; i < len; i ++ ) {
            for (int j = 0; j < width; j ++ ) {
                if (grid[i][j] == 1) continue;
                this.valid = 1;
                dfs(grid, i, j);
                res += valid;
            }
        }
        return res;
    }

    public void dfs(int[][] grid, int x, int y) {
        if (x < 0 || y < 0 || x >= grid.length || y >= grid[0].length) {
            this.valid = 0;
            return;
        }
        if (grid[x][y] == 1) {
            return;
        }
        grid[x][y] = 1;
        dfs(grid, x - 1, y);
        dfs(grid, x + 1, y);
        dfs(grid, x, y + 1);
        dfs(grid, x, y - 1);
    }
}
```

