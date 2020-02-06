# 63 不同路径 II

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

网格中的障碍物和空位置分别用 1 和 0 来表示。

说明：m 和 n 的值均不超过 100。

```text
示例 1:

输入: [ 
 [0,0,0],
 [0,1,0], 
 [0,0,0] 
 ]

输出: 2 

解释: 
3x3 网格的正中间有一个障碍物。 
从左上角到右下角一共有 2 条不同的路径： 1. 向右 -> 向右 -> 向下 -> 向下 
2. 向下 -> 向下 -> 向右 -> 向右
```

思路和62一样，只是多加了障碍物的处理罢了

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] map) {
       
        int iLen = map.length;
        int jLen = map[0].length;
        if (map[0][0] == 1 || map[iLen - 1][jLen - 1] == 1) {
            return 0;
        }
        int dp[] = new int[jLen];
        dp[0] = 1;
        for (int j = 1; j < jLen; j++) {
            if (map[0][j] == 0 && dp[j - 1] == 1) {
                dp[j] = 1;
            } else {
                break;
            } 
        }
        for (int i = 1; i < iLen; i++) {
            if (map[i][0] == 0 && dp[0] == 1) {
                dp [0] = 1;
            } else {
                dp [0] = 0;
            }
            for (int j = 1; j < jLen; j++) {
                if (map[i][j] == 0) {
                    dp[j] = dp[j - 1] + dp[j];
                } else {
                    dp[j] = 0;
                }
                
            }
        }
        return dp[jLen -1];


    }
}
```

