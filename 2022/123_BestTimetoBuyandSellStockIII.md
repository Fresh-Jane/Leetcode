### 123. Best Time to Buy and Sell Stock III (Hard)

https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/

```
// Bidirectional DP
// lw record the max profit can gain from index zero to i, rw record the max profit from i to n.
// Divid and conquer, we can reduce the repetitive calculation using DP.
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        const int n = prices.size();
        if (n == 0) return 0;
        vector<int> lw(n, 0), rw(n, 0);
        int min_p = prices[0], max_p = prices[n-1];
        for (int i = 1; i < n; ++i) {
            lw[i] = max(lw[i-1], prices[i] - min_p);
            min_p = min(min_p, prices[i]);
            int r = n - i - 1;
            rw[r] = max(rw[r+1], max_p - prices[r]);
            max_p = max(max_p, prices[r]);
        }
        int res = max(rw[0], lw[n-1]);
        for (int i = 0; i < n-1; ++i) res = max(res, lw[i]+rw[i+1]);
        return res;
    }
};
```
