### 1042. Flower Planting With No Adjacent (Medium)

https://leetcode.com/problems/flower-planting-with-no-adjacent/description/

```
class Solution {
public:
    
    vector<int> gardenNoAdj(int n, vector<vector<int>>& paths) {
        vector<int> res(n, 0);
        vector<vector<int>> path_m(n+1);
        for (const vector<int>& p : paths) {
            path_m[p[0]].push_back(p[1]);
            path_m[p[1]].push_back(p[0]);
        }
        for (int i = 1; i <= n; ++i) {
            vector<int> color(5, 0);
            for (int ni : path_m[i]) color[res[ni-1]] = 1;
            for (int c = 1; c <= 4; ++c) if (!color[c]) res[i-1] = c;
        }
        return res;
    }
};
```
