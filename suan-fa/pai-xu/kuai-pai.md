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








