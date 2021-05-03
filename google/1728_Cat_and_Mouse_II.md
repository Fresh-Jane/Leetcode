### 1728 Cat and Mouse II

https://leetcode.com/problems/cat-and-mouse-ii/

```
class Solution {
public:
    int dp[71][8][8][8][8];
    int cm, mm;
    int m, n;
    int go[4][2] = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
    bool dfs(const vector<string>& grid, int t, int ci, int cj, int mi, int mj) {
        if (t % 2) {
            if (ci == mi && cj == mj) return false;
            if (grid[ci][cj] == 'F') return false;
            if (grid[mi][mj] == 'F') return true;
            if (t >= 70) return false;
        } else {
            if (ci == mi && cj == mj) return true;
            if (grid[ci][cj] == 'F') return true;
            if (grid[mi][mj] == 'F') return false;
            if (t >= 70) return true;
        }
        if (dp[t][ci][cj][mi][mj] != -1) return dp[t][ci][cj][mi][mj];
        
        int who = t % 2;
        bool win = false;
        if (who == 0) { // Cat is next
            for (int i = 0; i < 4; ++i) {
                for (int j = 0; j <= cm; ++j) {
                    int ni = ci + go[i][0] * j, nj = cj + go[i][1] * j;
                    if (ni >= 0 && ni < m && nj >= 0 && nj < n && grid[ni][nj] != '#') {
                        if (!dfs(grid, t + 1, ni, nj, mi, mj)) {
                            win = true;
                            break;
                        }
                    } else {
                        break;
                    }
                    if (win) break;
                }
            }
        } else {
            for (int i = 0; i < 4; ++i) {
                for (int j = 0; j <= mm; ++j) {
                    int ni = mi + go[i][0] * j, nj = mj + go[i][1] * j;
                    if (ni >= 0 && ni < m && nj >= 0 && nj < n && grid[ni][nj] != '#') {
                        if (!dfs(grid, t + 1, ci, cj, ni, nj)) {
                            win = true;
                            break;
                        }
                    } else {
                        break;
                    }
                    if (win) break;
                }
            }
        }
        dp[t][ci][cj][mi][mj] = win;
        return dp[t][ci][cj][mi][mj];
    }
    
    bool canMouseWin(vector<string>& grid, int catJump, int mouseJump) {
        memset(dp, -1, sizeof(dp));
        cm = catJump;
        mm = mouseJump;
        m = grid.size();
        n = grid[0].size();
        int ci, cj, mi, mj;
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (grid[i][j] == 'C') {
                    ci = i;
                    cj = j;
                }
                if (grid[i][j] == 'M') {
                    mi = i;
                    mj = j;
                }
            }
        }
        return dfs(grid, 1, ci, cj, mi, mj);
    }
};
```
