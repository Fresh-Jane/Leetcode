### 542. 01 Matrix (Medium)

https://leetcode.com/problems/01-matrix/

```
// Space: O(1)
class Solution {
public:
    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
        if (mat.empty()) return mat;
        int m = mat.size(), n = mat[0].size();
        for (int i = 0; i < m; ++i)
            for (int j = 0; j < n; ++j)
                if (mat[i][j]) mat[i][j] = INT_MAX;
                
        queue<pair<int, int>> q;
        for (int i = 0; i < m; ++i)
            for (int j = 0; j < n; ++j)
                if (mat[i][j] == 0) q.push({i, j});
        vector<int> go{1, 0, -1, 0, 1};
        int level = 0;
        while(!q.empty()) {
            int len = q.size();
            while(len--) {
                auto [x, y] = q.front(); q.pop();
                for (int i = 0; i < 4; ++i) {
                    int nx = x + go[i], ny = y + go[i + 1];
                    if (nx < 0 || nx >= m || ny < 0 || ny >= n || mat[nx][ny] != INT_MAX) continue;
                    mat[nx][ny] = level + 1;
                    q.push({nx, ny});
                }
            }
            level++;
        }
        return mat;
    }
};

// Space: O(mn)
class Solution {
public:
    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
        const vector<int> go{1, 0, -1, 0, 1};
        const int m = mat.size(), n = mat[0].size();
        vector<vector<int>> res(m, vector<int>(n, m+n));
        queue<pair<int, int>> q;
        for(int i = 0; i < m; ++i) for (int j = 0; j < n; ++j) 
            if (mat[i][j] == 0) {
                q.push({i, j});
                res[i][j] = 0;
            }
        int dis = 1;
        while(!q.empty()) {
            int len = q.size();
            while(len--) {
                auto [x, y] = q.front(); q.pop();
                for(int i = 0; i < 4; ++i) {
                    const int nx = x + go[i], ny = y + go[i+1];
                    if (nx < 0 || nx >= m || ny < 0 || ny >= n) continue;
                    if (res[nx][ny] <= dis) continue;
                    q.push({nx, ny});
                    res[nx][ny] = dis;
                }
            }
            dis++;
        }    
        return res;
    }
};
```
