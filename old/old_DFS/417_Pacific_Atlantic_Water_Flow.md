### 417. Pacific Atlantic Water Flow (Medium)

Given an m x n matrix of non-negative integers representing the height of each unit cell in a continent, the "Pacific ocean" touches the left and top edges of the matrix and the "Atlantic ocean" touches the right and bottom edges.

Water can only flow in four directions (up, down, left, or right) from a cell to another one with height equal or lower.

Find the list of grid coordinates where water can flow to both the Pacific and Atlantic ocean.

Note:

- The order of returned grid coordinates does not matter.
- Both m and n are less than 150.
 

Example:

```
Given the following 5x5 matrix:

  Pacific ~   ~   ~   ~   ~ 
       ~  1   2   2   3  (5) *
       ~  3   2   3  (4) (4) *
       ~  2   4  (5)  3   1  *
       ~ (6) (7)  1   4   5  *
       ~ (5)  1   1   2   4  *
          *   *   *   *   * Atlantic

Return:

[[0, 4], [1, 3], [1, 4], [2, 2], [3, 0], [3, 1], [4, 0]] (positions with parentheses in above matrix).
```
```
// DFS
class Solution {
public: 
    int go[4][2] = {{0, -1}, {-1, 0}, {1, 0}, {0, 1}};
    int m = 0, n = 0;
    vector<vector<int>> reach;
    void dfs(const vector<vector<int>>& matrix, int x, int y, int val) {
        reach[x][y] |= val;
        for (int i = 0; i < 4; ++i) {
            const int nx = x + go[i][0], ny = y + go[i][1];
            if (nx < 0 || nx >= m || ny < 0 || ny >= n || 
                matrix[nx][ny] < matrix[x][y] || 
                (reach[nx][ny]&val) == val) continue;
            dfs(matrix, nx, ny, val);
        }
    }
    
    vector<vector<int>> pacificAtlantic(vector<vector<int>>& matrix) {
        if (matrix.empty()) return {};
        m = matrix.size();
        n = matrix[0].size();
        reach.resize(m, vector<int>(n, 0));
        for (int i = 0; i < m; ++i) dfs(matrix, i, 0, 1);
        for (int i = 1; i < n; ++i) dfs(matrix, 0, i, 1);
        
        for (int i = 0; i < m; ++i) dfs(matrix, i, n - 1, 2);
        for (int i = 0; i < n - 1; ++i) dfs(matrix, m - 1, i, 2);
        
        vector<vector<int>> res;
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j)
                if (reach[i][j] == 3) res.push_back({i, j});
        
        return res;
    }
};

// BFS
class Solution {
public: 
    int go[4][2] = {{0, -1}, {-1, 0}, {1, 0}, {0, 1}};
    int m = 0, n = 0;

    void bfs(const vector<vector<int>>& matrix, 
             vector<vector<int>>& reach, 
             queue<vector<int>>& visit, 
             int val) {
        while(!visit.empty()) {
            vector<int> cur_point = visit.front();
            visit.pop();
            const int cx = cur_point[0], cy = cur_point[1];
            reach[cx][cy] |= val;
            for (int i = 0; i < 4; ++i) {
                const int nx = cx + go[i][0];
                const int ny = cy + go[i][1];
                if (nx < 0 || nx >= m || ny < 0 || ny >= n || 
                    matrix[nx][ny] < matrix[cx][cy] ||
                    (reach[nx][ny]&val) == val) 
                    continue;
                visit.push({nx, ny});
            }
        }
    }
    
    vector<vector<int>> pacificAtlantic(vector<vector<int>>& matrix) {
        if (matrix.empty()) return {};
        m = matrix.size();
        n = matrix[0].size();
        vector<vector<int>> reach(m, vector<int>(n, 0));
        queue<vector<int>> visit;
        for (int i = 0; i < m; ++i) visit.push({i, 0});
        for (int i = 1; i < n; ++i) visit.push({0, i});
        bfs(matrix, reach, visit, 1);
        for (int i = 0; i < m; ++i) visit.push({i, n - 1});
        for (int i = 0; i < n - 1; ++i) visit.push({m - 1, i});
        bfs(matrix, reach, visit, 2);
        vector<vector<int>> res;
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (reach[i][j] == 3) res.push_back({i, j});
        return res;
    }
};
```
