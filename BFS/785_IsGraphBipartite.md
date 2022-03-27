### 785. Is Graph Bipartite (Medium)

https://leetcode.com/problems/is-graph-bipartite/

```
class Solution {
public:
    vector<int> color;
    bool isBipartite(vector<vector<int>>& graph) {
        const int n = graph.size();
        color.resize(n, -1);
        for (int i = 0; i < n; ++i) 
            if (color[i] == -1 && !isValid(graph, i, 0)) return false;
        return true;
    }
    
    bool isValid(const vector<vector<int>>& graph, int cur, int c) {
        color[cur] = c;
        for (const int next : graph[cur]) {
            if (color[next] == 1 - c) continue;
            if (color[next] == c || !isValid(graph, next, 1 - c)) return false;
        }
        return true;
    }
};
```
