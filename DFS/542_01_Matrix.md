### 542. 01 Matrix (Medium)

Given a matrix consists of 0 and 1, find the distance of the nearest 0 for each cell.

The distance between two adjacent cells is 1.

Example 1:

```
Input:
[[0,0,0],
 [0,1,0],
 [0,0,0]]

Output:
[[0,0,0],
 [0,1,0],
 [0,0,0]]
```
Example 2:

```
Input:
[[0,0,0],
 [0,1,0],
 [1,1,1]]

Output:
[[0,0,0],
 [0,1,0],
 [1,2,1]]
```

Note:

- The number of elements of the given matrix will not exceed 10,000.
- There are at least one 0 in the given matrix.
- The cells are adjacent in only four directions: up, down, left and right.

```
// BFS
class Solution {
public:
    vector<vector<int>> updateMatrix(vector<vector<int>>& matrix) {
        if (matrix.empty()) return {};
        int go[4][2] = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
        const int m = matrix.size(), n = matrix[0].size();
        vector<vector<int>> res(m, vector<int>(n, 0));
        queue<vector<int>> q;
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (matrix[i][j] == 0) q.push({i, j});
        int level = 0;
        while(!q.empty()) {
            int cnt = q.size();
            level++;
            while(cnt--) {
                vector<int> p = q.front(); q.pop();
                for (int i = 0; i < 4; ++i) {
                    int nx = p[0] + go[i][0];
                    int ny = p[1] + go[i][1];
                    if (nx < 0 || nx >= m || ny < 0 || ny >= n || matrix[nx][ny] != 1) continue;
                    res[nx][ny] = level;
                    matrix[nx][ny] = 2;
                    q.push({nx, ny});
                }
            } 
        }
        return res;
    }
};

// DP
class Solution 2 {
public:
    vector<vector<int>> updateMatrix(vector<vector<int>>& matrix) {
        if (matrix.empty()) return {};
        const int m = matrix.size(), n = matrix[0].size();
        vector<vector<int>> dp(m, vector<int>(n, 0));
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (matrix[i][j] == 1) dp[i][j] = m + n;
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (i > 0 && dp[i][j] > dp[i-1][j] + 1) dp[i][j] = dp[i-1][j] + 1;
                if (j > 0 && dp[i][j] > dp[i][j-1] + 1) dp[i][j] = dp[i][j-1] + 1;
            }
        }
        for (int i = m - 1; i >= 0; --i) {
            for (int j = n - 1; j >= 0; --j) {
                if (i < m - 1 && dp[i][j] > dp[i+1][j] + 1) dp[i][j] = dp[i+1][j] + 1;
                if (j < n - 1 && dp[i][j] > dp[i][j+1] + 1) dp[i][j] = dp[i][j+1] + 1;
            }
        }      
        return dp;
    }
};
```
