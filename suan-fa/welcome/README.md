---
description: 'permutations, combinations'
---

# 排列、组合 模板

{% code title="排列" %}
```python
nums    候选数字
deepth  当前递归深度
n       每个排列长度
used    标记是否用过

全排列情况下可简化deepth为cur.lenght, n为nums.length

P(nums, deepth, n, used, cur, ans):
    if deepth == n:
        ans.append(cur)
        return
    
    for i = 0 to nums.lenght:
        if used[i]: continue
        used[i] == true
        cur.append(nums[i])
        P(nums, deepth + 1, n, used, cur, ans)
        used[i] == false
        cur.pop()
        
P([1, 2, 3], 0, 3, [false * 3], [], ans)
输出
[
  [1,2,3], [1,3,2], [2,1,3],
  [2,3,1], [3,1,2], [3,2,1]
]

P([1, 2, 3], 0, 2, [false * 3], [], ans)
输出
[
  [1,2], [1,3], [2,1],
  [2,3], [3,1], [3,2]    
]
```
{% endcode %}

{% code title="组合" %}
```python
n    每个组合结果长度
s    从第s个元素开始取出元素来组合，只能取s之后的

C(nums, deepth, n, s, cur, ans):
    if deepth == n:
        ans.append(cur)
        reurn
    for i = s to nums.lenght:
        cur.append(nums[i])
        C(nums, deepth + 1, n, s + 1, cur, ans)
        cur.pop()

P([1, 2, 3], 0, 3, 0, [], ans)  
输出
[[1,2,3]]
  
P([1, 2, 3], 0, 2, 0, [], ans)
输出
[
  [1,2], [1,3], [2,3]
]
 
   
```
{% endcode %}

