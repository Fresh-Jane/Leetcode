### 286. Walls and Gates (Medium)

https://leetcode.com/problems/walls-and-gates/

```
// BFS
// We search the rooms from each door by level. So the nearest distance for each empty room is the distance when we first time we reach them. 
class Solution {
public:
    void wallsAndGates(vector<vector<int>>& rooms) {
        const int m = rooms.size(), n = rooms[0].size();
        vector<int> go{1, 0, -1, 0, 1};
        queue<pair<int, int>> q;
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (rooms[i][j] == 0) q.push({i, j});
        int level = 1;
        while(!q.empty()) {
            int len = q.size();
            while(len--) {
                const auto [x, y] = q.front(); q.pop();
                for (int i = 0; i < 4; ++i) {
                    const int nx = x + go[i], ny = y + go[i+1];
                    if (nx < 0 || nx >= m || ny < 0 || ny >= n) continue;
                    if (rooms[nx][ny] != 2147483647) continue;
                    rooms[nx][ny] = level;
                    q.push({nx, ny});
                }
            }
            level++;
        }   
    }
};
```
