### 827. Making A Large Island (Hard)

https://leetcode.com/problems/making-a-large-island/

```
class Solution {
public:
    int n;
    int go[5] = {1, 0, -1, 0, 1};
    int val;
    int dfs(vector<vector<int>>& grid, int x, int y) {
        int res = 1;
        grid[x][y] = val;
        for (int i = 0; i < 4; ++i) {
            const int nx = x + go[i], ny = y + go[i+1];
            if (nx < 0 || nx >= n || ny < 0 || ny >= n || grid[nx][ny] != 1) continue;
            res += dfs(grid, nx, ny);
        }
        return res;
    }
    int largestIsland(vector<vector<int>>& grid) {
        n = grid.size();
        val = 2;
        unordered_map<int, int> area;
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < n; ++j) {
                if (grid[i][j] == 1) {
                    area[val] = dfs(grid, i, j);
                    val++;
                }
            }
        }
        int res = 0;
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < n; ++j) {
                if (grid[i][j] == 0) {
                    int a = 1;
                    unordered_set<int> m;
                    for (int k = 0; k < 4; ++k) {
                        int ni = i + go[k], nj = j + go[k+1];
                        if (ni >= 0 && ni < n && nj >= 0 && nj < n) {
                            const int cur_v = grid[ni][nj];
                            if (cur_v > 1 && !m.count(cur_v)) {
                                m.insert(cur_v);
                                if (area.count(cur_v))
                                    a += area[cur_v];
                            }
                        }
                    }
                    res = std::max(res, a);
                } else {
                    if (area.count(grid[i][j])) {
                        res = std::max(res, area[grid[i][j]]);
                    }
                }
            }
        }
        return res;
    }
};

// 1st wrong solution
class Solution {
public:
    int n;
    int go[5] = {1, 0, -1, 0, 1};
    void dfs(vector<vector<int>>& grid, int val, int x, int y, int& num) {
        grid[x][y] = val;
        num++;
        for (int i = 0; i < 4; ++i) {
            const int nx = x + go[i], ny = y + go[i+1];
            if (nx >= 0 && nx < n && ny >= 0 && ny < n && grid[nx][ny] == 1) {
                dfs(grid, val, nx, ny, num);
            }
        }
    }
    int largestIsland(vector<vector<int>>& grid) {
        n = grid.size();
        int val = 2;
        unordered_map<int, std::vector<int>> m;
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < n; ++j) {
                if (grid[i][j] == 1) {
                    int num = 0;
                    dfs(grid, val, i, j, num);
                    m[val] = {i, j, num};
                    val++;
                }
            }
        }
        int res = 0;
        for (auto p : m) {
            int cur_res = p.second[2] + 1;
            const int cur_val = grid[p.second[0]][p.second[1]];
            queue<pair<int, int>> q;
            q.push(make_pair(p.second[0], p.second[1]));
            while(!q.empty()) {
                auto cur = q.front();
                q.pop();
                const int x = cur.first, y = cur.second;
                for (int i = 0; i < 4; ++i) {
                    int nx = x + go[i], ny = y + go[i+1];
                    std::cout << nx << " " << ny << std::endl;
                    if(nx >= 0 && nx < n && ny >= 0 && ny < n) {
                        if (grid[x][y] == cur_val && grid[nx][ny] == 0) {
                            q.push(make_pair(nx, ny));
                        } else if (grid[x][y] == 0 && grid[nx][ny] != 0 && grid[nx][ny] != cur_val) {
                            cur_res = std::max(cur_res, p.second[2] + m[grid[nx][ny]][2] + 1);
                        }
                    }
                }
            }
            res = std::max(res, cur_res);
        }
        return res;
    }
}; 
```
