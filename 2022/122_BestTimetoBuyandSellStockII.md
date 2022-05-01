### 122. Best Time to Buy and Sell Stock II (Medium)

https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/

```
// Greedy
// Add all increasing subarrays
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int res = 0;
        for (int i = 1; i < prices.size(); ++i)
            if (prices[i] > prices[i-1]) res += prices[i] - prices[i-1];
        return res;
    }
};
```
