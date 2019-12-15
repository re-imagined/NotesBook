# 212 单词搜索II

给定一个二维网格和一个单词，找出该单词是否存在于网格中。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

```text
输入
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]
输出: ["eat","oath"]
```

> 提**示:**
>
> 你需要优化回溯算法以通过更大数据量的测试。你能否早点停止回溯？ 如果当前单词不存在于所有单词的前缀中，则可以立即停止回溯。什么样的数据结构可以有效地执行这样的操作？散列表是否可行？为什么？ 前缀树如何？
>
> 如果你想学习如何实现一个基本的前缀树，请先查看这个问题： [实现Trie（前缀树）](https://leetcode-cn.com/problems/implement-trie-prefix-tree/description/)。

> **方法1：**
>
> 使用DFS遍历所有board和单词
>
> 时间复杂度 O\(sum\(m  _n_  4 ^ len\(word\)\)\)
>
> 空间复杂度 O\(l\)



> **方法2:**
>
> 构建一个字典树，然后用DFS在字典树种搜索，可以在有相同前缀的单词时节省时间
>
> 时间复杂度 O\(m n 4 ^ len\(word\)\) 
>
> 空间复杂度 O\(sum\(l\)\)

{% tabs %}
{% tab title="DFS" %}
```java
class Solution {
    int l;
    int h;
    public List<String> findWords(char[][] board, String[] words) {
        l = board.length;
        h = board[0].length;
        List<String> res = new ArrayList<>();
        for (String word : words) {
            boolean found = false;
            for (int x = 0; x < l; x ++) {
                for (int y = 0; y < h; y ++) {
                    if (dfs(board, 0, x, y, word)) {
                        res.add(word);
                        found = true;
                    }
                   if (found) break;
                }
                if (found) break;
            }
        }

        return res;
    }

    boolean dfs(char[][] board, int depth, int x, int y, String word) {
        if(x < 0 || y < 0 || x >= l || y >= h || word.charAt(depth) != board[x][y]) return false;

        if (depth == word.length() - 1) return true;
        char tmp = board[x][y];
        board[x][y] = '0';
        boolean res = dfs(board, depth + 1, x + 1, y, word) ||
            dfs(board, depth + 1, x - 1, y, word) ||
            dfs(board, depth + 1, x, y + 1, word) ||
            dfs(board, depth + 1, x, y - 1, word);
        board[x][y] = tmp;
        return res;
    }
}
```
{% endtab %}

{% tab title="Trie" %}
```java
class Solution {
    int l;
    int h;
    public List<String> findWords(char[][] board, String[] words) {
        WordTried tree = new WordTried();
        for (String word : words) {
            tree.insert(word);
        }
        Set<String> resSet = new HashSet<>();
        l = board.length;
        h = board[0].length;
        for (int x = 0; x < l; x ++) {
            for (int y = 0; y < h; y ++) {
                search(board, tree.root, x, y, resSet);
            }
        }
        return new ArrayList<>(resSet);
    }

    private void search(char[][] board, TrieNode cur, int x, int y, Set<String> resSet) {
     
        if (x >= l || x < 0 || y >= h || y < 0 || board[x][y] == '0') return;
        cur = cur.children[board[x][y] - 'a'];
        if (cur == null) {
            return;
        }
        if (cur.val != null){
            resSet.add(cur.val);
            cur.val = null;
        }
   
        char tmp = board[x][y];
        board[x][y] = '0';
        search(board, cur, x + 1, y, resSet);
        search(board, cur, x - 1, y, resSet);
        search(board, cur, x, y + 1, resSet);
        search(board, cur, x, y - 1, resSet);
        board[x][y] = tmp;
    }
    
    class TrieNode {
        private String val;
        private TrieNode[] children = new TrieNode[26];
    }
    
    class WordTried {
        TrieNode root = new TrieNode();
        public void insert(String word) {
            TrieNode cur = root;
            for (char c : word.toCharArray()) {
                if (cur.children[c - 'a'] == null) {
                    cur.children[c - 'a'] = new TrieNode();
                }
                cur = cur.children[c - 'a'];
            }
            cur.val = word;
        }
    }
}
```
{% endtab %}
{% endtabs %}



