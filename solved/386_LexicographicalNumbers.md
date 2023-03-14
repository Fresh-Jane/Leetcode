### 386. Lexicographical Numbers (Medium)

https://leetcode.com/problems/lexicographical-numbers/

```
// DFS
class Solution {
public:
    vector<int> lexicalOrder(int n) {
        vector<int> res;
        for (int i = 1; i <= 9; ++i) dfs(i, n, res);
        return res;
    }
    void dfs(int cur, int n, vector<int>& res) { 
        if (cur > n) return;
        res.push_back(cur);
        for (int i = 0; i <= 9; ++i) {
            if (cur * 10 + i > n) return;
            dfs(cur * 10 + i, n, res);
        }
    }
};
```
