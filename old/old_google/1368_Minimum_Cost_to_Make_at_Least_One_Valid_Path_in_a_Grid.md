### 1368. Minimum Cost to Make at Least One Valid Path in a Grid (Hard)

Given a m x n grid. Each cell of the grid has a sign pointing to the next cell you should visit if you are currently in this cell. The sign of grid[i][j] can be:
1 which means go to the cell to the right. (i.e go from grid[i][j] to grid[i][j + 1])
2 which means go to the cell to the left. (i.e go from grid[i][j] to grid[i][j - 1])
3 which means go to the lower cell. (i.e go from grid[i][j] to grid[i + 1][j])
4 which means go to the upper cell. (i.e go from grid[i][j] to grid[i - 1][j])
Notice that there could be some invalid signs on the cells of the grid which points outside the grid.

You will initially start at the upper left cell (0,0). A valid path in the grid is a path which starts from the upper left cell (0,0) and ends at the bottom-right cell (m - 1, n - 1) following the signs on the grid. The valid path doesn't have to be the shortest.

You can modify the sign on a cell with cost = 1. You can modify the sign on a cell one time only.

Return the minimum cost to make the grid have at least one valid path.

Example 1:

```
Input: grid = [[1,1,1,1],[2,2,2,2],[1,1,1,1],[2,2,2,2]]
Output: 3
Explanation: You will start at point (0, 0).
The path to (3, 3) is as follows. (0, 0) --> (0, 1) --> (0, 2) --> (0, 3) change the arrow to down with cost = 1 --> (1, 3) --> (1, 2) --> (1, 1) --> (1, 0) change the arrow to down with cost = 1 --> (2, 0) --> (2, 1) --> (2, 2) --> (2, 3) change the arrow to down with cost = 1 --> (3, 3)
The total cost = 3.
```
Example 2:

```
Input: grid = [[1,1,3],[3,2,2],[1,1,4]]
Output: 0
Explanation: You can follow the path from (0, 0) to (2, 2).
```
Example 3:

```
Input: grid = [[1,2],[4,3]]
Output: 1
```
Example 4:

```
Input: grid = [[2,2,2],[2,2,2]]
Output: 3
```
Example 5:

```
Input: grid = [[4]]
Output: 0
```

Constraints:

- m == grid.length
- n == grid[i].length
- 1 <= m, n <= 100

```
// DP & 0/1 BFS
// Time: O(MN)
// Space: O(MN)
class Solution {
public:
    int m, n;
    int go[4][2] = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
    void dfs(const vector<vector<int>>& grid, int x, int y, vector<vector<int>>& dp, int cost, queue<pair<int,int>>& q) {
        if (x < 0 || x >= m || y < 0 || y >= n || dp[x][y] != INT_MAX) return;
        dp[x][y] = cost;
        q.push(make_pair(x, y));
        const int dir = grid[x][y] - 1;
        dfs(grid, x+go[dir][0], y+go[dir][1], dp, cost, q);
    }
    int minCost(vector<vector<int>>& grid) {
        m = grid.size();
        n = grid[0].size();
        vector<vector<int>> dp(m, vector<int>(n, INT_MAX));
        queue<pair<int,int>> q;
        int cost = 0;
        dfs(grid, 0, 0, dp, cost, q);
        while(!q.empty()) {
            cost++;
            const int size = q.size();
            for (int i = 0; i < size; ++i) {
                pair<int, int> pos = q.front();
                q.pop();
                for (int j = 0; j < 4; ++j) {
                    dfs(grid, pos.first+go[j][0], pos.second+go[j][1], dp, cost, q);
                }
            }
        }
        return dp[m-1][n-1];
    }
};

// Dijkstra
// Time: O(MN)
// Space: O(MN)
class Solution {
public:
    int minCost(vector<vector<int>>& grid) {
        constexpr int go[4][2] = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
        const int m = grid.size(), n = grid[0].size();
        vector<vector<bool>> vis(m, vector<bool>(n, false));
        using S = tuple<int, int, int>;
        priority_queue<S, vector<S>, greater<S>> q;
        q.push({0, 0, 0});
        while(!q.empty()) {
            auto [c, i, j] = q.top(); q.pop();
            if (vis[i][j]) continue;
            vis[i][j] = true;
            if (i == m - 1 && j == n - 1) return c;
            for (int d = 0; d < 4; ++d) {
                const int ni = i + go[d][0], nj = j + go[d][1];
                if (ni < 0 || ni >= m || nj < 0 || nj >= n) continue;
                if (vis[ni][nj]) continue;
                int nc = c;
                if (grid[i][j] != d + 1) ++nc;
                q.push({nc, ni, nj});
            }
        }
        return -1;
    }
};
```
