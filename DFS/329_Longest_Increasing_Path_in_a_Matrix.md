### 329. Longest Increasing Path in a Matrix (Hard)

Given an integer matrix, find the length of the longest increasing path.

From each cell, you can either move to four directions: left, right, up or down. You may NOT move diagonally or move outside of the boundary (i.e. wrap-around is not allowed).

Example 1:

```
Input: nums = 
[
  [9,9,4],
  [6,6,8],
  [2,1,1]
] 
Output: 4 
Explanation: The longest increasing path is [1, 2, 6, 9].
```
Example 2:

```
Input: nums = 
[
  [3,4,5],
  [3,2,6],
  [2,2,1]
] 
Output: 4 
Explanation: The longest increasing path is [3, 4, 5, 6]. Moving diagonally is not allowed.
```
```
class Solution {
public:
    int go[4][2] = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    int m, n;
    int dfs(const vector<vector<int>>& matrix, int x, int y, vector<vector<int>>& memo) {
        if (memo[x][y]) return memo[x][y];
        int max_path = 1;
        for (int i = 0; i < 4; ++i) {
            const int nx = x + go[i][0], ny = y + go[i][1];
            if (nx < 0 || nx >= m || ny < 0 || ny >= n || matrix[nx][ny] <= matrix[x][y]) continue;
            max_path = std::max(dfs(matrix, nx, ny, memo) + 1, max_path);
        }
        memo[x][y] = max_path;
        return max_path;
    }
    
    int longestIncreasingPath(vector<vector<int>>& matrix) {
        if (matrix.empty()) return 0;
        int max_path = 1;
        m = matrix.size();
        n = matrix[0].size();
        vector<vector<int>> memo(m, vector<int>(n, 0));
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                max_path = std::max(dfs(matrix, i, j, memo), max_path);
        return max_path;
    }
};
```
