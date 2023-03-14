### 256. Paint House (Medium)

https://leetcode.com/problems/paint-house/

```
// DP
class Solution {
public:
    int minCost(vector<vector<int>>& costs) {
        const int n = costs.size();
        vector<vector<int>> dp(2, vector<int>(3, 0));
        dp[0] = costs[0];
        for (int i = 1, in = 1; i < n; ++i, in = 1-in) {
            dp[in][0] = min(dp[1-in][1], dp[1-in][2]) + costs[i][0];
            dp[in][1] = min(dp[1-in][0], dp[1-in][2]) + costs[i][1];
            dp[in][2] = min(dp[1-in][1], dp[1-in][0]) + costs[i][2];
        }
        return min(dp[(n-1)%2][0], min(dp[(n-1)%2][1], dp[(n-1)%2][2]));
    }
};
```
