### 348. Design Tic-Tac-Toe (Medium)

https://leetcode.com/problems/design-tic-tac-toe/description/

```
// Time: O(1)
// Space: O(N)
class TicTacToe {
public:
    TicTacToe(int n) {
        this->n = n;
        rows.resize(n, 0);
        cols.resize(n, 0);
        diagonal = anti_diagonal = 0;
    }
    
    int move(int row, int col, int player) {
        int val = (player == 1) ? 1 : -1;
        rows[row] += val;
        cols[col] += val;
        if (row == col) diagonal += val;
        if (row == n - 1 - col) anti_diagonal += val;
        if (rows[row] == n || cols[col] == n || diagonal == n || anti_diagonal == n) return 1;
        if (rows[row] == -n || cols[col] == -n || diagonal == -n || anti_diagonal == -n) return 2;
        return 0;
    }
private:
    vector<int> rows, cols;
    int diagonal, anti_diagonal, n;
};

/**
 * Your TicTacToe object will be instantiated and called as such:
 * TicTacToe* obj = new TicTacToe(n);
 * int param_1 = obj->move(row,col,player);
 */
```
