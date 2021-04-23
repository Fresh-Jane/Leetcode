### 329. Longest Increasing Path in a Matrix (Hard)

Given an m x n integers matrix, return the length of the longest increasing path in matrix.

From each cell, you can either move in four directions: left, right, up, or down. You may not move diagonally or move outside the boundary (i.e., wrap-around is not allowed).

Example 1:

```
Input: matrix = [[9,9,4],[6,6,8],[2,1,1]]
Output: 4
Explanation: The longest increasing path is [1, 2, 6, 9].
```
Example 2:

```
Input: matrix = [[3,4,5],[3,2,6],[2,2,1]]
Output: 4
Explanation: The longest increasing path is [3, 4, 5, 6]. Moving diagonally is not allowed.
```
Example 3:

```
Input: matrix = [[1]]
Output: 1
```

Constraints:

- m == matrix.length
- n == matrix[i].length
- 1 <= m, n <= 200
- 0 <= matrix[i][j] <= 2^31 - 1

```
// Memorize DFS
class Solution {
public:
    vector<int> go = {-1, 0, 1, 0, -1};
    int m, n;
    int dfs(vector<vector<int>>& matrix, int x, int y, vector<vector<int>>& memo) {
        if (memo[x][y]) return memo[x][y];
        int res = 1;
        for (int i = 0; i < 4; ++i) {
            int nx = x + go[i];
            int ny = y + go[i+1];
            if (nx >= m || nx < 0 || ny >= n || ny < 0 || matrix[nx][ny] <= matrix[x][y]) continue;
            res = max(dfs(matrix, nx, ny, memo) + 1, res);
        }
        memo[x][y] = res;
        return memo[x][y];
    }
    
    int longestIncreasingPath(vector<vector<int>>& matrix) {
        m = matrix.size();
        n = matrix[0].size();
        vector<vector<int>> memo(m, vector<int>(n, 0));
        int res = 1;
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                res = max(dfs(matrix, i, j, memo), res);
        return res;
    }
};
```
