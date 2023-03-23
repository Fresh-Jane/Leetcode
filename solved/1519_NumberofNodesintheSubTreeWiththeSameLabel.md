### 1519. Number of Nodes in the Sub-Tree With the Same Label (Medium)

https://leetcode.com/problems/number-of-nodes-in-the-sub-tree-with-the-same-label/description/

```
class Solution {
public:
    vector<vector<int>> tree_e;
    vector<int> countSubTrees(int n, vector<vector<int>>& edges, string labels) {
        tree_e.resize(n);
        for (const vector<int>& d : edges) {
            tree_e[d[0]].push_back(d[1]);
            tree_e[d[1]].push_back(d[0]);
        }
        vector<int> res(n, 0);
        dfs(0, labels, res);
        return res;
    }

    vector<int> dfs(int cur, const string& labels, vector<int>& res) {
        vector<int> cnt(26, 0);
        res[cur] = 1;
        cnt[labels[cur]-'a'] = 1;
        for (const int nc : tree_e[cur]) {
            if (res[nc]) continue;
            vector<int> n_cnt = dfs(nc, labels, res);
            for (int i = 0; i < 26; ++i) cnt[i] += n_cnt[i];
        }
        res[cur] = cnt[labels[cur]-'a'];
        return cnt;
    }
};
```
