# 
## Problem
[1143. Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)

## Solution 
- dynamic programming. DP[i][j] represents the longest common subsequence of text1[0 ... i] & text2[0 ... j].

## Code
```python
# Top Down DP
# time complexity O(MN)
# space complexity O(MN)
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        M, N = len(text1), len(text2)
        from functools import lru_cache
        @lru_cache(None)
        def dp(i,j):
            if i<0 or j<0: return 0
            if text1[i]==text2[j]:return dp(i-1,j-1)+1
            return max(dp(i-1, j), dp(i, j-1))
        return dp(M-1, N-1)
```
