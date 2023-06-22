### 51. N-Queens (Hard)

https://leetcode.com/problems/n-queens/description/

```
class Solution {
public:
    vector<vector<string>> solveNQueens(int n) {
        if (n <= 0) return {};
        vector<vector<string>> res;
        vector<string> puzzle(n, string(n, '.'));
        dfs(0, n, puzzle, res);
        return res;
    }
    void dfs(int row, int n, vector<string>& puzzle, vector<vector<string>>& res) {
        if (row == n) {
            res.push_back(puzzle);
            return;
        }
        for (int j = 0; j < n; ++j) {
            puzzle[row][j] = 'Q';
            if (valid(puzzle, row, j, n)) dfs(row+1, n, puzzle, res);
            puzzle[row][j] = '.';
        }
    }
    bool valid(const vector<string>& puzzle, int row, int col, int n) {
        for (int i = 0; i < row; ++i) if (puzzle[i][col] == 'Q') return false;
        for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; --i, --j) if (puzzle[i][j] == 'Q') return false; // This should be &&, not ,
        for (int i = row - 1, j = col + 1; i >= 0 && j < n; --i, ++j) if (puzzle[i][j] == 'Q') return false;
        return true;
    }
};
```
