### 529. Minesweeper (Medium)

https://leetcode.com/problems/minesweeper/

```
// DFS
class Solution {
public:
    int m, n;
    vector<int> go{1, 0, -1, 0, 1, -1, -1, 1, 1};
    vector<vector<char>> updateBoard(vector<vector<char>>& board, vector<int>& click) {
        if (board.empty()) return board;
        m = board.size();
        n = board[0].size();
        dfs(board, click[0], click[1]);
        return board;
    }

    void dfs(vector<vector<char>>& board, int x, int y) {
        if (board[x][y] == 'M') {
            board[x][y] = 'X';
            return;
        }
        int c = 0;
        for (int i = 0; i < 8; ++i) {
            const int nx = x + go[i], ny = y + go[i+1];
            if (nx >= 0 && nx < m && ny >= 0 && ny < n && board[nx][ny] == 'M') ++c;
        }
        if (c) {
            board[x][y] = '0' + c;
            return;
        }
        board[x][y] = 'B';
        for (int i = 0; i < 8; ++i) {
            const int nx = x + go[i], ny = y + go[i+1];
            if (nx >= 0 && nx < m && ny >= 0 && ny < n && board[nx][ny] == 'E') dfs(board, nx, ny);
        }
    }
};
```
