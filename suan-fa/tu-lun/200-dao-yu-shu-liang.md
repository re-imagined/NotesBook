# 200 岛屿数量

给定一个由 '1'（陆地）和 '0'（水）组成的的二维网格，计算岛屿的数量。一个岛被水包围，并且它是通过水平方向或垂直方向上相邻的陆地连接而成的。你可以假设网格的四个边均被水包围。

```text
输入:
11110
11010
11000
00000

输出: 1

输入:
11000
11000
00100
00011

输出: 3
```

```java
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        int count = 0;
    
        for (int i = 0; i < grid.size(); i++) {
            for (int j = 0; j < grid[0].size(); j++) {
                if (grid[i][j] == '1') {
                    count ++;
                    dfs(grid, i, j);
                } 
            }
        }
        return count;
    }

private:
    void dfs(vector<vector<char>>& grid, int x, int y) {
        if (x < 0|| y < 0 || x >= grid.size() || y >= grid[0].size() 
                || grid[x][y] == '0') {
            return;
        }
        grid[x][y] = '0';
        dfs(grid, x + 1, y);
        dfs(grid, x - 1, y);
        dfs(grid, x, y + 1);
        dfs(grid, x, y - 1);
    }
};
```

