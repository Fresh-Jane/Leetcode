### 568. Maximum Vacation Days (Hard)

https://leetcode.com/problems/maximum-vacation-days/

```
// DP
// Time: O(KN^2), Space: O(KN)
class Solution {
public:
    int maxVacationDays(vector<vector<int>>& flights, vector<vector<int>>& days) {
        const int n = flights.size(), k = days[0].size();
        vector<vector<int>> dp(k+1, vector<int>(n, -1));
        dp[0][0] = 0;
        for (int i = 1; i <= k; ++i) {
            for(int j = 0; j < n; ++j) {
                for (int pre = 0; pre < n; ++pre) {
                    if ((pre == j || flights[pre][j]) && (dp[i-1][pre] != -1)) 
                        dp[i][j] = max(dp[i][j], dp[i-1][pre] + days[j][i-1]);
                }
            }
        }
        int res = 0;
        for (int i = 0; i < n; ++i) res = max(res, dp[k][i]);
        return res;
    }
};
```
