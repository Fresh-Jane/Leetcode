### 797. All Paths From Source to Target (Medium)

https://leetcode.com/problems/all-paths-from-source-to-target/

```
class Solution {
public:
    void dfs(const vector<vector<int>>& graph, int s, int e, vector<int> r, vector<vector<int>>& res) {
        if (s == e) {
            res.push_back(r);
            return;
        } 
        for (int next : graph[s]) {
            r.push_back(next);
            dfs(graph, next, e, r, res);
            r.pop_back();
        }
    } 
    
    vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& graph) {
        vector<vector<int>> res;
        vector<int> r;
        r.push_back(0);
        dfs(graph, 0, graph.size()-1, r, res);
        return res;
    }
};
```
