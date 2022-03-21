### 399. Evaluate Division (Medium)

https://leetcode.com/problems/evaluate-division/

```
// First, we should convert the equations into a graph.
// Then using dfs to calculate each quary.
class Solution {
public:
    unordered_map<string, vector<pair<string, double>>> m;
    vector<double> calcEquation(vector<vector<string>>& equations, vector<double>& values, vector<vector<string>>& queries) {
        for (int i = 0; i < equations.size(); ++i) {
            const string a = equations[i][0], b = equations[i][1];
            m[a].push_back({b, values[i]});
            m[b].push_back({a, 1.0 / values[i]});
        }
        unordered_map<string, bool> visit;
        vector<double> res;
        for (int i = 0; i < queries.size(); ++i) {
            const string c = queries[i][0], d = queries[i][1];
            double r = 1.0;
            visit.clear();
            if (!m.count(c) || 
                !m.count(d) ||
                !dfs(visit, c, d, r)) res.push_back(-1.0);
            else res.push_back(r);
        }
        return res;
    }
    
    bool dfs(unordered_map<string, bool>& visit, const string& start, const string& end, double& r) {
        if (start == end) return true;
        visit[start] = true;
        for (auto p : m[start]) {
            if (!visit[p.first]) {
                r *= p.second;
                if (dfs(visit, p.first, end, r)) return true;
                r /= p.second;
            }
        }
        return false;
    }
}; 
```
