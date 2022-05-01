### 419. Battleships in a Board (Medium)

https://leetcode.com/problems/battleships-in-a-board/

```
// Just count the head of the ships.
class Solution {
public:
    int countBattleships(vector<vector<char>>& board) {
        int res = 0;
        const int m = board.size(), n = board[0].size();
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (board[i][j] == 'X' && 
                    (i == 0 || board[i-1][j] != 'X') &&
                    (j == 0 || board[i][j-1] != 'X')) 
                    res++;
        return res;
    }
};


// Flood fill, DFS
class Solution {
public:
    vector<int> go{1, 0, -1, 0, 1};
    int m, n;
    int countBattleships(vector<vector<char>>& board) {
        int res = 0;
        m = board.size(), n = board[0].size();
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (board[i][j] == 'X') {
                    res++;
                    dfs(board, i, j);
                }
            }
        }
        return res;
    }
    
    void dfs(vector<vector<char>>& board, int x, int y) {
        board[x][y] = '.';
        for (int i = 0; i < 4; ++i) {
            const int nx = x + go[i], ny = y + go[i+1];
            if (nx < 0 || nx >= m || ny < 0 || ny >= n) continue;
            if (board[nx][ny] != 'X') continue;
            dfs(board, nx, ny);
        }
    }
};
```
