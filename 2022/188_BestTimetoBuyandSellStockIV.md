### 188. Best Time to Buy and Sell Stock IV (Hard)

https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/

```
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        const int n = prices.size();
        if (n <= 0 || k <= 0) return 0;
        if (2*k > n) {
            int res = 0;
            for (int i = 1; i < prices.size(); ++i) 
                res += max(0, prices[i]-prices[i-1]);
            return res;
        }
        vector<vector<vector<int>>> dp(n, vector<vector<int>>(k+1, vector<int>(2, -100000000)));
        dp[0][0][0] = 0;
        dp[0][1][1] = -prices[0];
        for(int i = 1; i < n; ++i) {
            for (int j = 0; j <= k; ++j) {
                dp[i][j][0] = max(dp[i-1][j][0], dp[i-1][j][1]+prices[i]);
                if (j > 0)
                    dp[i][j][1] = max(dp[i-1][j-1][0]-prices[i], dp[i-1][j][1]);
            }
        }
        int res = 0;
        for (int j = 0; j <= k; ++j) 
            res = max(res, dp[n-1][j][0]);
        return res;
    }
};
```
