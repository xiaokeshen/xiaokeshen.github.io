## Longest Common Subsequence

## Problem 

[300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)

## Solution  

dynamic programming. 
- States
DP[i] represents the longest increasing subsequence ends at nums[i].
- transitions: max(dp[j]+1 for j in range(i) if nums[j]>nums[i].

## Code 

```python
# bottom up DP
# time complexity O(n^2)
# space complexity O(n)
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        if not nums:return 0
        N = len(nums)
        dp = [1]*N
        for i in range(1, N):
            num = nums[i]
            for j in range(i):
                if num > nums[j]:
                    dp[i] = max(dp[i], dp[j]+1)
        return max(dp)
```
