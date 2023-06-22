### 52. N-Queens II (Hard)

https://leetcode.com/problems/n-queens-ii/description/

```
class Solution {
public:
    int totalNQueens(int n) {
        if (n <= 0) return 0;
        if (n == 1) return 1;
        int res = 0;
        vector<string> board(n, string(n, '.'));
        dfs(board, 0, n, res);
        return res;
    }
    void dfs(vector<string>& board, int row, int n, int& res) {
        if (row == n) {
            res++;
            return;
        }
        for (int i = 0; i < n; ++i) {
            board[row][i] = 'Q';
            if (valid(board, row, i, n)) dfs(board, row+1, n, res);
            board[row][i] = '.';
        }
    }
    bool valid(vector<string>& board, int row, int col, int n) {
        for (int i = 0; i < row; ++i) if (board[i][col] == 'Q') return false;
        for (int i = row-1, j = col-1; i >= 0 && j >= 0; --i, --j) if (board[i][j] == 'Q') return false;
        for (int i = row-1, j = col+1; i >= 0 && j < n; --i, ++j) if (board[i][j] == 'Q') return false;
        return true;
    }
};
```
