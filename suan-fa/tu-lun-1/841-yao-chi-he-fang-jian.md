---
description: DFS BFS
---

# 841 钥匙和房间

有 N 个房间，开始时你位于 0 号房间。每个房间有不同的号码：0，1，2，...，N-1，并且房间里可能有一些钥匙能使你进入下一个房间。

在形式上，对于每个房间 i 都有一个钥匙列表 rooms\[i\]，每个钥匙 rooms\[i\]\[j\] 由 \[0,1，...，N-1\] 中的一个整数表示，其中 N = rooms.length。 钥匙 rooms\[i\]\[j\] = v 可以打开编号为 v 的房间。

最初，除 0 号房间外的其余所有房间都被锁住。

你可以自由地在房间之间来回走动。

如果能进入每个房间返回 true，否则返回 false。

> 提示
>
> 1. `1 <= rooms.length <= 1000`
> 2. `0 <= rooms[i].length <= 1000`
> 3. 所有房间中的钥匙数量总计不超过 `3000`。

```text
输入: [[1],[2],[3],[]]
输出: true
解释:  
我们从 0 号房间开始，拿到钥匙 1。
之后我们去 1 号房间，拿到钥匙 2。
然后我们去 2 号房间，拿到钥匙 3。
最后我们去了 3 号房间。
由于我们能够进入每个房间，我们返回 true。

输入：[[1,3],[3,0,1],[2],[0]]
输出：false
解释：我们不能进入 2 号房间。
```

{% tabs %}
{% tab title="DFS" %}
```java
class Solution {
    public boolean canVisitAllRooms(List<List<Integer>> rooms) {
        if (rooms.size() == 0) {
            return true;
        }
        int[] visited = new int[rooms.size()];
        dfs(rooms, visited, 0);
        for (int i : visited) {
            if (i == 0) {
                return false;
            }
        }
        return true;
    }

    private void dfs(List<List<Integer>> rooms, int[] visited, int start) {
        if (visited[start] == 1) {
            return;
        }
        visited[start] = 1;
        for (int i = 0; i < rooms.get(start).size(); i++) {
            int nextRoom = rooms.get(start).get(i);
            dfs(rooms, visited, nextRoom);
        }
    }
}
```
{% endtab %}

{% tab title="BFS" %}
```java
class Solution {
    public boolean canVisitAllRooms(List<List<Integer>> rooms) {
        int roomCount = rooms.size();
        if (roomCount <= 1) {
            return true;
        }
        boolean[] visited = new boolean[roomCount];
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(0);
        visited[0] = true;
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                int key = queue.poll();
                List<Integer> nexts = rooms.get(key);
                for (Integer next : nexts) {
                    if (!visited[next]) {
                        queue.offer(next);
                        visited[next] = true;
                    }
                }
            }
        }
        for (boolean v : visited) {
            if (!v) {
                return false;
            }
        }
        return true;
    }
}
```
{% endtab %}
{% endtabs %}

