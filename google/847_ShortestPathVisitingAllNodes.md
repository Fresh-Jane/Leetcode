### 847. Shortest Path Visiting All Nodes (Hard)

https://leetcode.com/problems/shortest-path-visiting-all-nodes/

```
class Solution {
public:
    int shortestPathLength(vector<vector<int>>& graph) {
        int n = graph.size();
        int full = (1 << n) - 1;
        
        queue<S> q;
        unordered_set<S, Shash, Sequal> m(8, Shash(), Sequal());
        
        for (int i = 0; i < n; ++i) {
            S s = {i, 1 << i, 0};
            q.push(s);
            m.insert(s);
        }
        
        while(!q.empty()) {
            S s = q.front(); q.pop();
            if (s.path == full) return s.length;
            for (const int nr : graph[s.node]) {
                S ns = {nr, s.path | 1 << nr, s.length+1};
                if (!m.count(ns)) {
                    q.push(ns);
                    m.insert(ns);
                }
            }
        }
        return -1;
    }
private:
    struct S {
        int node = 0;
        int path = 0;
        int length = 0;
    };
    struct Shash {
        size_t operator()(const S& s) const {
            return hash<int>()(s.node) ^ hash<int>()(s.path);
        }
    };
    struct Sequal {
        bool operator()(const S& s1, const S& s2) const {
            return s1.node == s2.node && s1.path == s2.path;
        }
    };
};
```
