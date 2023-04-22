### 886. Possible Bipartition (Medium)

https://leetcode.com/problems/possible-bipartition/

```
class Solution {
public:
    vector<int> color;
    vector<vector<int>> dis_map;
    bool possibleBipartition(int n, vector<vector<int>>& dislikes) {
        color.resize(n+1, -1);
        dis_map.resize(n+1);
        for (const vector<int>& dis : dislikes) {
            dis_map[dis[0]].push_back(dis[1]);
            dis_map[dis[1]].push_back(dis[0]);
        }
        for (int i = 1; i <= n; ++i) {
            if (color[i] == -1 && !dfs(i, 0)) return false;
        }
        return true;
    }
    bool dfs(int i, int c) {
        color[i] = c;
        for (int j : dis_map[i]) {
            if (color[j] == 1-c) continue;
            if (color[j] == c || !dfs(j, 1-c)) return false;
        }
        return true;
    }
};
```
