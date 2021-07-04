### 983. Minimum Cost For Tickets (Medium)

https://leetcode.com/problems/minimum-cost-for-tickets/

```
https://leetcode.com/problems/minimum-cost-for-tickets/discuss/226659/Two-DP-solutions-with-pictures
// DP for all calendar days
// Time: O(N) all calendar days
// Space: O(366)
class Solution {
public:
    int mincostTickets(vector<int>& days, vector<int>& costs) {
        unordered_set<int> travel(days.begin(), days.end());
        int res[366] = {};
        for (int i = 1; i < 366; ++i) {
            if (!travel.count(i)) res[i] = res[i-1];
            else {
                res[i] = min({res[i-1] + costs[0], 
                              res[max(0, i-7)] + costs[1], 
                              res[max(0, i-30)] + costs[2]});
            }
        }
        return res[days.back()];
    }
};

// DP for only travel days
// Time: O(n) travel day num
// Space: O(38)
class Solution {
public:
    int mincostTickets(vector<int>& days, vector<int>& costs) {
        queue<pair<int, int>> last7, last30;
        int cost = 0;
        for (const int d : days) {
            while (!last7.empty() && last7.front().first + 7 <= d) last7.pop();
            while (!last30.empty() && last30.front().first + 30 <= d) last30.pop();
            last7.push({d, cost + costs[1]});
            last30.push({d, cost + costs[2]});
            cost = min({cost + costs[0], last7.front().second, last30.front().second});
        }
        return cost;
    }
};
```
