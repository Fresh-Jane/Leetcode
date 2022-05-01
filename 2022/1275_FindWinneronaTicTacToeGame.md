### 1275. Find Winner on a Tic Tac Toe Game (Easy)

https://leetcode.com/problems/find-winner-on-a-tic-tac-toe-game/

```
class Solution {
public:
    string tictactoe(vector<vector<int>>& moves) {
        vector<vector<char>> grid(3, vector<char>(3, ' '));
        for (int i = 0; i < moves.size(); ++i) {
            const int x = moves[i][0], y = moves[i][1];
            grid[x][y] = i % 2 ? 'O' : 'X';
            if (hasWin(grid, x, y)) return i % 2 ? "B" : "A";
        }
        return moves.size() == 9 ? "Draw" : "Pending";
    }
    bool hasWin(vector<vector<char>> grid, int x, int y) {
        if (grid[x][0] == grid[x][1] && grid[x][0] == grid[x][2]) return true;
        if (grid[0][y] == grid[1][y] && grid[0][y] == grid[2][y]) return true;
        if (x == y && grid[0][0] == grid[1][1] && grid[1][1] == grid[2][2]) return true;
        if (x + y == 2 && grid[0][2] == grid[1][1] && grid[0][2] == grid[2][0]) return true;
        return false;
    }
};
```
