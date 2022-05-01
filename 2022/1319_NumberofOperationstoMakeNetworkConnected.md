### 1319. Number of Operations to Make Network Connected (Medium)

https://leetcode.com/problems/number-of-operations-to-make-network-connected/

```
// Union find.
// We know that the minimum number of edges required for a graph with n nodes to remain connected is n-1. So similarly, if there are k components in a disconnected graph, we need at least k-1 edges. 
class Solution {
public:
    vector<int> root;
    int find(int x) {
        if (root[x] != x) root[x] = find(root[x]);
        return root[x];
    }
    void link(int x, int y) {
        const int rx = find(x);
        const int ry = find(y);
        if (rx != ry) root[ry] = rx;
    }
    int makeConnected(int n, vector<vector<int>>& connections) {
        if (connections.size() < n - 1) return -1;
        root.resize(n, 0);
        for (int i = 0; i < n; ++i) root[i] = i;
        for (const auto& con : connections) link(con[0], con[1]);
        unordered_set<int> res;
        for (int i = 0; i < n; ++i) res.insert(find(root[i]));
        return res.size() - 1;
    }
};
```
