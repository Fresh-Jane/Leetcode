### 802. Find Eventual Safe States (Medium)

https://leetcode.com/problems/find-eventual-safe-states/description/

```
// Topology sort
class Solution {
public:
    vector<int> eventualSafeNodes(vector<vector<int>>& graph) {
        const int n = graph.size();
        vector<int> out(n);
        vector<vector<int>> in(n);
        for (int i = 0; i < n; ++i) 
            for (int n : graph[i]) {
                out[i]++;
                in[n].push_back(i);
            }
        queue<int> q;
        vector<int> res;
        for (int i = 0; i < n; ++i) if (out[i] == 0) q.push(i);
        while(!q.empty()) {
            int cur = q.front(); q.pop();
            res.push_back(cur);
            for (int next : in[cur]) if (--out[next] == 0) q.push(next);
        }
        sort(res.begin(), res.end());
        return res;
    }
};
```
