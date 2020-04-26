## Summary of Dynamic Problems

| Problem       | State         | Transitions                                                                     | Time        | Space|
| ------------- |---------------| --------------------------------------------------------------------------------|-------------|------|
| [LIS](classical/lcs.md)       | (i, j)        | dp[i-1][j-1]+1 if text1[i]==text2[j], max(dp[i-1][j], dp[i][j-1]), otherwise    |O(NM)        | O(NM)|
