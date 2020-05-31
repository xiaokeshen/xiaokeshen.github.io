# LCS style problems

## Problem
[LeetCode 72. Edit Distance](https://leetcode.com/problems/edit-distance/)
## Solution
For i, j positions char form word1 and word2, we have several actions:
if word1[i] == word2[j], we move forward one step
if word1[i] != word2[j]:
- delete word1[i], then result will be 1+dp(i+!1, j)
- delete word2[j], then result will be 1+dp(i, j+1)
- replace word1[i] to word2[j] or the opposite way: 1 + dp(i+1, j+1)
```python
# time complexity: O(mn)
# Space complexity: O(mn)
from functools import lru_cache
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        N1, N2 = len(word1), len(word2)
        @lru_cache(None)
        def dp(i, j):
            if i==N1 or j==N2:return max(N1-i, N2-j)
            if word1[i]==word2[j]:
                return dp(i+1, j+1)
            return min(dp(i+1, j), dp(i, j+1), dp(i+1, j+1))+1
        return dp(0, 0)
```
