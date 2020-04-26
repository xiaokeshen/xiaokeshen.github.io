## Summary of Dynamic Problems
| Problem       | State         | Transitions                                                                     | Time        | Space|
| --- |---| ---|---|---|
| [LIS](classical/lis.md)       | (i)        | all j<i    |O(n^2)      | O(n)|
| [LCS](classical/lcs.md)       | (i, j)        | dp[i-1][j-1]+1 if text1[i]==text2[j] <br> max(dp[i-1][j], dp[i][j-1]), otherwise.    |O(NM)        | O(NM)|
[//]: <>| [TSP](https://medium.com/analytics-vidhya/are-you-read-for-solving-the-traveling-salesman-problem-80e3c4ea45fc)       |(pos, mask)       | all n cities    |O(2^nn^2)        | O(n2^n)|
