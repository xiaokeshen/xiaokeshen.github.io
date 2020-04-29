## Binary trees

Most binary tree problems can be solved by using recursion.

## Binary Tree Maximum Path Sum
- [Binary Tree Maximum Path Sum](https://leetcode.com/explore/featured/card/30-day-leetcoding-challenge/532/week-5/3314/)

## Solution  

For each node, we can compute the max left SIMPLE path sum L and max right SIMPLE path sum R. Here SIMPLE path means this path can still be explored by this node's parent node. As L and R might be negative, for the max path sum contains this node will be:
max(node.val, node.val+L, node.val+R, node.val+L+R)
max SIMPLE path sum  for this node will be: max(node.val, node.val+L, node.val+R). It excludes the node.val+L+R as in this case, the  path can not be explored by this node's parent node.

```python
Time complexity: O(n)
As we are using LRU_cache to save the results for each node, the Space complexity is also O(n)
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxPathSum(self, root: TreeNode) -> int:
        self.res = -float('inf')
        from functools import lru_cache
        @lru_cache(None)
        def get_max(node):
            if node is None:return -float('inf')
            l, r = get_max(node.left), get_max(node.right)
            val = node.val
            this_res = max(val, val + l, val + r, val + l + r)
            self.res = max(self.res, this_res)
            return max(val, val + l, val + r)
        get_max(root)
        return self.res
```

Thanks for reading. 

