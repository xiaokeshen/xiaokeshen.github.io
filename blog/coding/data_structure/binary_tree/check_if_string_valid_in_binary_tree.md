# Check If a String Is a Valid Sequence from Root to Leaves Path in a Binary Tree

## Problem
- [Check If a String Is a Valid Sequence from Root to Leaves Path in a Binary Tree](https://leetcode.com/explore/featured/card/30-day-leetcoding-challenge/532/week-5/3315/)

## Solution  

```python
# time complexity: O(n)
# space complexity: O(1)
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isValidSequence(self, root: TreeNode, arr: List[int]) -> bool:
        def check(node, i):
            if i==len(arr)-1:
                return node is not None and node.val==arr[-1] and node.left is None and node.right is None
            if not node:return False
            if node.val==arr[i]:
                return check(node.left,i+1) or check(node.right, i+1)
            else:return False 
        return check(root, 0)
```

The above solution works with the constraints that the start point MUST be the root. If we do not have this constraints, we can use the following code:

```python
# at the beginning: if arr[0]=node.val, we can choose to pick up this node or not pick up this node. The complexity of this one will be higher.
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isValidSequence(self, root: TreeNode, arr: List[int]) -> bool:
        def check(node, i):
            if i==len(arr)-1:
                return node is not None and node.val==arr[-1] and node.left is None and node.right is None
            if not node:return False
            if i==0:
                if node.val==arr[i]:
                    return check(node.left, 1) or check(node.right, 1) or check(node.left, 0) or check(node.right, 0)
                else:return check(node.left, 0) or check(node.right, 0)
            else:
                if node.val == arr[i]:
                    return check(node.left,i+1) or check(node.right, i+1)
                else:return False
        return check(root, 0)

```
