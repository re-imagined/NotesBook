# 378 有序矩阵中第K小的元素

给定一个 n x n 矩阵，其中每行和每列元素均按升序排序，找到矩阵中第k小的元素。 请注意，它是排序后的第k小元素，而不是第k个元素。

示例:

```text
matrix = [ [ 1, 5, 9], [10, 11, 13], [12, 13, 15] ], k = 8,
返回 13。
```



```java
class Solution {
    public int kthSmallest2(int[][] matrix, int k) {
        // 最大堆
        PriorityQueue<Integer> pq = new PriorityQueue<>((i, j) -> -i + j);
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                pq.add(matrix[i][j]);
                if (pq.size() > k) {
                    pq.poll();
                }
            }
        }
        return pq.poll();
    }

    public int kthSmallest(int[][] matrix, int k) {
        int left = matrix[0][0];
        int len = matrix.length;
        int right = matrix[len - 1][len - 1]; 
        
        while (left < right) {
            int mid = (left + right) / 2;
            int count = getCountNotLargerThan(matrix, mid);
            if (count < k) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        return right;
    }

    // 从矩阵的左下角开始找，把每列小于等于target的数量加入count，
    // 最后得出小于这个target的元素个数
    private int getCountNotLargerThan(int[][] matrix, int tartget) {
        int i = matrix.length - 1;
        int j = 0;
        int count = 0;
        while (i >= 0 && j < matrix.length) {
            if (matrix[i][j] <= tartget) {
                count += i + 1;
                j++;
            } else {
                i--;
            }
        }
        return count;
    }
}
```

