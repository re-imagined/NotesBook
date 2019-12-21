# 841 钥匙和房间

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
public void bfs(List<List<Integer>> rooms) {
    Queue<Integer> queue = new LinkedList<>();
    queue.offer(0);
    List<Integer> room;
    while(!queue.isEmpty()) {
        int roomNum = queue.poll();
        room = rooms.get(roomNum);
        visited[roomNum] = true;
        for(int key : room)
            if(!visited[key])
                queue.offer(key);
    }
}
```
{% endtab %}
{% endtabs %}

