### 130. Surrounded Regions (Medium)

Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

Example:

```
X X X X
X O O X
X X O X
X O X X
```
After running your function, the board should be:

```
X X X X
X X X X
X X X X
X O X X
```
Explanation:

Surrounded regions shouldn’t be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically.

```
class Solution {
public:
    int m, n;
    void dfs(vector<vector<char>>& board, int i, int j) {
        if (board[i][j] == 'O') {
            board[i][j] = 'T';
            // This is a trick to avoid stack overflow (runtime error) in LC
            if (i > 1) dfs(board, i - 1, j);
            if (i + 1 < m) dfs(board, i + 1, j);
            if (j > 1) dfs(board, i, j - 1);
            if (j + 1 < n) dfs(board, i, j + 1);
        }
    }
    void solve(vector<vector<char>>& board) {
        if (board.empty()) return;
        m = board.size(), n = board[0].size();
        for (int i = 0; i < n; ++i) {
            if (board[0][i] == 'O') dfs(board, 0, i);
            if (board[m - 1][i] == 'O') dfs(board, m - 1, i);
        }
        for (int i = 0; i < m; ++i) {
            if (board[i][0] == 'O') dfs(board, i, 0);
            if (board[i][n - 1] == 'O') dfs(board, i, n - 1);
        }
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (board[i][j] == 'O') board[i][j] = 'X';
                else if (board[i][j] == 'T') board[i][j] = 'O';
            }
        }
    }
};
```

