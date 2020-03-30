# 快排

## 快排

### 时间复杂度

**最好情况：**分割点每次都是中位数 

T\(n\) = 2 \* T\(n/2\) + O\(n\) = O\(nlogn\)

2 \* T\(n/2\)  表示每次调用两个递归，每个递归的分割点都正好都把空间平分

O\(n\) 表示分割空间的操作（partition），线性复杂度

**最坏情况：**

T\(n\)  = T\(n - 1\) + T\(1\) + O\(n\)

T\(n - 1\) + T\(1\) 表示每次分割点都是空间的最小或最大值，完全没起到分割的作用

**不好不坏的情况：**

T\(n\) = T\(n/10\) + T\(n/9\) + O\(n\) = O\(nlogn\)

T\(n/10\) + T\(n/9\)  表示按1比9的比例划分空间，或者是任意一种可能的比例，只要不太坏



### 空间复杂度

**Best /Average ：**

O\(logn\) \* 1 = O\(logn\)

O\(logn\) 表示递归深度，每次都是对半分

1表示每次递归需要的空间大小

{% code title="伪代码" %}
```text
quick_sort(array, start, end):
    p = partition(array, start, end)
    quick_sort(array, start, p)
    quick_sort(array, p + 1, end)
```
{% endcode %}

```java
class Solution {
    public List<Integer> sortArray(int[] nums) {
        
        if (nums == null || nums.length <= 0) {
            return new ArrayList();
        }

        sort(nums, 0, nums.length - 1);
        List<Integer> list2 = new ArrayList<Integer>();
        for (int num : nums) {
            list2.add(num);
        }
        return list2;        
    }
    
    private void sort(int[] nums, int start, int end) {
        if (start >= end) {
            return;
        }
        int p = partition(nums, start, end);
        sort(nums, start, p - 1);
        sort(nums, p + 1, end);
    }

    private int partition(int[] nums, int start, int end) {
        int i = start;
        int j = start + 1;
        int v = nums[start];
        while (true) {
            while (nums[++i] < v) {
                if (i == end) {
                    break;
                }
            }

            while (nums[--j] > v) {
                if (j == start) {
                    break;
                }
            }
            if (i >= j) {
                break;
            }
            int tmp = nums[i];
            nums[i] = nums[j];
            nums[j] = tmp;
        }
        int tmp = nums[start];
        nums[start] = nums[j];
        nums[j] = tmp;
        return j;

    }
    



}java
```





