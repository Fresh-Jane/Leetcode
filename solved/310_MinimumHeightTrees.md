### 310. Minimum Height Trees (Medium)

https://leetcode.com/problems/minimum-height-trees/

```
class Solution {
public:
    vector<int> findMinHeightTrees(int n, vector<vector<int>>& edges) {
        if (n == 1) return {0};
        vector<vector<int>> graph(n, vector<int>());
        vector<int> indegree(n);
        for (const auto& e : edges) {
            graph[e[0]].push_back(e[1]);
            graph[e[1]].push_back(e[0]);
            indegree[e[0]]++;
            indegree[e[1]]++;
        }
        queue<int> q;
        for (int i = 0; i < n; ++i) if (indegree[i] == 1) q.push(i);
        vector<int> res;
        while(!q.empty()) {
            int len = q.size();
            vector<int> leaves;
            while(len--) {
                const int cur = q.front(); q.pop();
                leaves.push_back(cur);
                for (const int next : graph[cur]) if (--indegree[next] == 1) q.push(next);
            }
            res = leaves;
        }
        return res;
    }
};
```
