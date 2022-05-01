### 261. Graph Valid Tree (Medium)

https://leetcode.com/problems/graph-valid-tree/

```
// BFS
class Solution {
public:
    bool validTree(int n, vector<vector<int>>& edges) {
        if (n == 1 && edges.empty()) return true;
        if (edges.size() != n - 1) return false;
        vector<vector<int>> graph(n);
        vector<int> indegree(n);
        for (const auto e : edges) {
            graph[e[0]].push_back(e[1]);
            graph[e[1]].push_back(e[0]);
            indegree[e[0]]++;
            indegree[e[1]]++;
        }
        int valid_num = 0;
        queue<int> q;
        for (int i = 0; i < n; ++i) if (indegree[i] == 1) q.push(i);
        while(!q.empty()) {
            const int cur = q.front(); q.pop();
            valid_num++;
            for(int next : graph[cur]) if (--indegree[next] == 1) q.push(next);
        }
        return valid_num == n;
    }
};
```
