# 105 从前序与中序遍历序列构造二叉树

根据一棵树的前序遍历与中序遍历构造二叉树。

**注意:**  
你可以假设树中没有重复的元素。

例如，给出

```text
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
```

返回如下的二叉树：

```text
    3
   / \
  9  20
    /  \
   15   7
```

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    indexMap = {}
    
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        if (len(inorder) == 0):
            return None
        for i in range(len(inorder)):
            self.indexMap[inorder[i]] = i;
        return self.build(inorder, preorder);
    
    def build(self, inorder: List[int], preorder: List[int]) -> TreeNode:
        if len(inorder) == 0 or len(preorder) == 0:
            return None
        root = TreeNode(preorder[0])
        mid = inorder.index(preorder[0])
        root.left = self.build(inorder[:mid], preorder[1:mid+1])
        root.right = self.build(inorder[mid+1:], preorder[mid+1:])
        return root;
```





