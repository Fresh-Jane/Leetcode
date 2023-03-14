### 1615. Maximal Network Rank (Medium)

https://leetcode.com/problems/maximal-network-rank/

```
class Solution {
public:
    int maximalNetworkRank(int n, vector<vector<int>>& roads) {
        vector<unordered_set<int>> graph(n);
        for (int i = 0; i < roads.size(); ++i) {
            graph[roads[i][0]].insert(roads[i][1]);
            graph[roads[i][1]].insert(roads[i][0]);
        }
        int res = 0;
        for (int i = 0; i < n; ++i) {
            for (int j = i + 1; j < n; ++j) {
                if (i == j) continue;
                int cur_res = graph[i].size() + graph[j].size();
                if (graph[i].count(j)) --cur_res;
                res = max(res, cur_res);
            }
        }
        return res;
    }
};
```
