# 79 单词搜索

给定一个二维网格和一个单词，找出该单词是否存在于网格中。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

示例:

```text
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

给定 word = "ABCCED", 返回 true.
给定 word = "SEE", 返回 true.
给定 word = "ABCB", 返回 false.
```

{% tabs %}
{% tab title="dfs" %}
```java
/**
  时间复杂度 O(m * n * 4 ^ len(word))
  空间复杂度 O(1)
*/

class Solution {
    int h;
    int l;

    public boolean exist(char[][] board, String word) {
        if (board.length == 0) return false;
        h = board.length;
        l = board[0].length;
        for (int i = 0; i < h; i++) {
            for (int j = 0; j < l; j++) {
                if (search(board, word, 0, i, j)) return true;
            }
        }
        return false;
    }

    private boolean search(char[][] board, String word, int depth, int x, int y) {
        if (x < 0 || y < 0 || x >= h || y >= l || word.charAt(depth) != board[x][y]) {
            return false;
        }
        if (depth == word.length() - 1) {
            return true;
        }
        char tmp = board[x][y];
        board[x][y] = 0;
        boolean ret = search(board, word, depth + 1, x - 1, y)
                || search(board, word, depth + 1, x + 1, y)
                || search(board, word, depth + 1, x, y - 1)
                || search(board, word, depth + 1, x, y + 1);
        board[x][y] = tmp;
        return ret;
    }
}

```
{% endtab %}
{% endtabs %}



