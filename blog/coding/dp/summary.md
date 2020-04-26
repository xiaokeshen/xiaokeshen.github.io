## Summary of Dynamic Problems

| Problem       | State         | Transitions                                                                     | Time        | Space|
| --- |---| ---|---|------|
| [LIS](classical/lis.md)       | (i)        | all j<i    |O(n^2)        | O(n)|
| [LCS](classical/lcs.md)       | (i, j)        | dp[i-1][j-1]+1 if text1[i]==text2[j] <br> max(dp[i-1][j], dp[i][j-1]), otherwise.    |O(NM)        | O(NM)|
