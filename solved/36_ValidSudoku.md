### 36. Valid Sudoku (Medium)

https://leetcode.com/problems/valid-sudoku/description/

```
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        vector<vector<bool>> row(9, vector<bool>(9, false));
        vector<vector<bool>> col(9, vector<bool>(9, false));
        vector<vector<bool>> sub(9, vector<bool>(9, false));
        for (int i = 0; i < 9; ++i) {
            for (int j = 0; j < 9; ++j) {
                if (board[i][j] != '.') {
                    int cur = board[i][j] - '1';
                    int sub_id = (i/3) * 3 + j/3;
                    if (row[i][cur] || col[j][cur] || sub[sub_id][cur]) return false;
                    row[i][cur] = col[j][cur] = sub[sub_id][cur] = true;
                }
            }
        }
        return true;
    }
};
```
