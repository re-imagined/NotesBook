---
description: 记忆化递归
---

# 139 单词拆分

给定一个非空字符串 s 和一个包含非空单词列表的字典 wordDict，判定 s 是否可以被空格拆分为一个或多个在字典中出现的单词。

说明：

拆分时可以重复使用字典中的单词。 你可以假设字典中没有重复的单词。

```text
输入: s = "leetcode", wordDict = ["leet", "code"]
输出: true
解释: 返回 true 因为 "leetcode" 可以被拆分成 "leet code"。

输入: s = "applepenapple", wordDict = ["apple", "pen"]
输出: true
解释: 返回 true 因为 "applepenapple" 可以被拆分成 "apple pen apple"。
     注意你可以重复使用字典中的单词。

输入: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
输出: false
```

递归从每个位置拆分成左右两个字符串，并且用一个HashMap来缓存右侧子串是否在字典里面，

![](../../.gitbook/assets/image%20%288%29.png)

```java
class Solution {
    Set<String> wordSet;
    Map<String, Boolean> memory;

    public boolean wordBreak(String s, List<String> wordDict) {
        wordSet = new HashSet<>(wordDict);
        memory = new HashMap<>();
        return breakWord(s);
    }

    private boolean breakWord(String s) {
        if (memory.containsKey(s)) {
            return memory.get(s);
        }

        if (wordSet.contains(s)){
            memory.put(s, true);
            return true;
        }

        for (int i = 1; i < s.length(); i++) {
            String left = s.substring(0, i);
            String right = s.substring(i);
            if (breakWord(left) && wordSet.contains(right)) {
                memory.put(s, true);
                return true;
            }
        }
        memory.put(s, false);
        return false;

    }

}
```

