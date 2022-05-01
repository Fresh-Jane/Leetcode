### 309. Best Time to Buy and Sell Stock with Cooldown (Medium)

https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/

```
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        const int n = prices.size();
        if (n < 2) return 0;
        vector<vector<int>> dp(n, vector<int>(2, INT_MIN));
        dp[0][0] = 0;
        dp[0][1] = -prices[0];
        dp[1][1] = max(-prices[0], -prices[1]);
        dp[1][0] = max(prices[1] - prices[0], 0);
        for (int i = 2; i < n; ++i) {
            dp[i][0] = max(dp[i-1][1] + prices[i], dp[i-1][0]);
            dp[i][1] = max(dp[i-1][1], dp[i-2][0] - prices[i]);
        }
        return max(dp[n-1][0], dp[n-1][1]);
    }
};
```
