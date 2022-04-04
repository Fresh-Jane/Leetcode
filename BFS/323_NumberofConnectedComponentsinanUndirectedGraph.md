### 323. Number of Connected Components in an Undirected Graph (Medium)

https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/

```
// Union find
class Solution {
public:
    vector<int> pre;
    int find(int x) {
        if (pre[x] != x) pre[x] = find(pre[x]);
        return pre[x];
    }
    void link(int x, int y) {
        const int px = find(x), py = find(y);
        if (px != py) pre[py] = px; 
    }
    int countComponents(int n, vector<vector<int>>& edges) {
        pre.resize(n, 0);
        for (int i = 0; i < n; ++i) pre[i] = i;
        for (auto e : edges) link(e[0], e[1]);
        unordered_set<int> s;
        for (int i = 0; i < n; ++i) s.insert(find(pre[i]));
        return s.size();
    }
};
```
