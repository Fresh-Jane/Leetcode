### 130. Surrounded Regions (Medium)

https://leetcode.com/problems/surrounded-regions/

```
// DFS
class Solution {
public:
    int m, n;
    void dfs(vector<vector<char>>& board, int x, int y) {
        board[x][y] = 'T';
        int go[4][2] = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
        for (int i = 0; i < 4; ++i) {
            const int nx = x + go[i][0], ny = y + go[i][1];
            if (nx >= 0 && nx < m && ny >= 0 && ny < n && board[nx][ny] == 'O') dfs(board, nx, ny);
        }
    }
    void solve(vector<vector<char>>& board) {
        m = board.size();
        n = board[0].size();
        for (int i = 0; i < m; ++i) {
            if (board[i][0] == 'O') dfs(board, i, 0);
            if (board[i][n-1] == 'O') dfs(board, i, n-1);
        }
        for (int j = 1; j < n - 1; ++j) {
            if (board[0][j] == 'O') dfs(board, 0, j);
            if (board[m-1][j] == 'O') dfs(board, m-1, j);
        }    
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (board[i][j] == 'O') board[i][j] = 'X';
                if (board[i][j] == 'T') board[i][j] = 'O';
            }
        }
    }
};
```
