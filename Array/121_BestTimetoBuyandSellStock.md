### 121. Best Time to Buy and Sell Stock (Easy)

https://leetcode.com/problems/best-time-to-buy-and-sell-stock/

```
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if (prices.empty()) return 0;
        int min_p = prices[0], res = 0;
        for (int i = 1; i < prices.size(); ++i) {
            if (prices[i] > min_p) res = max(res, prices[i]-min_p);
            else if (prices[i] < min_p) min_p = prices[i];
        }
        return res;
    }
};
```
