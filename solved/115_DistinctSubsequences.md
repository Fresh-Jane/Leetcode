### 115. Distinct Subsequences (Hard)

https://leetcode.com/problems/distinct-subsequences/description/

```
class Solution {
public:
    using ll = long long;
    int numDistinct(string s, string t) {
        const int m = t.size(), n = s.size();
        vector<vector<ll>> dp(m+1, vector<ll>(n+1, 0));
        dp[0][0] = 1;
        for (int i = 1; i <= m; ++i) dp[i][0] = 0;
        for (int j = 1; j <= n; ++j) dp[0][j] = 1;
        for (int i = 1; i <= m; ++i) {
            for (int j = 1; j <= n; ++j) {
                if (dp[i][j-1] > INT_MAX) continue;
                dp[i][j] = dp[i][j-1];
                if (s[j-1] == t[i-1]) dp[i][j] += dp[i-1][j-1];
            }
        }
        return dp[m][n];
    }
};
```
