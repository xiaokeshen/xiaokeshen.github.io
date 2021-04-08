# Leetcode 1815. Maximum Number of Groups Getting Fresh Donuts  
## Problem  
[LC 1815 Maximum Number of Groups Getting Fresh Donuts](https://leetcode.com/contest/biweekly-contest-49/problems/maximum-number-of-groups-getting-fresh-donuts/)

## Explanation  
- Approach 1: We can solve it by using the permutation which has the complexity of O(n!). As n is 30, TLE.   
- Approach 2: [TSP](https://medium.com/analytics-vidhya/are-you-read-for-solving-the-traveling-salesman-problem-80e3c4ea45fc) similar. We can use a similar idea as TSP problem. The different of this problem to the TSP is we only need know a set of used nodes, we don't need to know which node is the last visited node. Based on this the TSP has the complexity of O(n^2*2^n), however, this one the complexity is O(n*2^n). This code can pass half of the test cases, still get TLE as n is too large.  
- Approach 3: Simulated annealing ([ant colony optimization algorithm](https://en.wikipedia.org/wiki/Ant_colony_optimization_algorithms)) :We can further use the simulate a simulated annealing algorithm to approximate the approach 2, which can help us get AC.

## Code   
### Approach 2 
```
42 / 72 test cases passed.
Status: Time Limit Exceeded
``` 
```cpp
/*
Time complexity: O(n*2^n)
Space complexity: O(2^n)
*/
class Solution {
public:
    int maxHappyGroups(int b, vector<int>& g) {
        const int n = g.size();
        if (b==1) return n;
        vector<int> dp(1<<n, 0);
        for (auto & x:g) x %= b;
        for (int i = 0; i < (1 << n); ++i) {
            int sum = 0;
            for (int j = 0; j < n; ++j) {
                if (i & (1 << j)) {
                    sum += g[j];
                }
            }
            for (int j = 0; j < n; ++j) {
                if (!(i & (1<<j))) {
                    auto newState = i | (1<<j);
                    dp[newState] = max(dp[newState], (sum%b == 0) + dp[i]);
                }
            }
        }
        return dp[(1<<n) - 1];
        
    }
};

``` 

## Approach 3 (To be added): 
```cpp
```
