### 79. Word Search (Medium)

https://leetcode.com/problems/word-search/description/

```
class Solution {
public:
    int m, n;
    vector<int> go{1, 0, -1, 0, 1};

    bool exist(vector<vector<char>>& board, string word) {
        if (board.empty() || word.empty()) return false;
        m = board.size(), n = board[0].size();
        if (m * n < (int)word.size()) return false;
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (board[i][j] == word[0] && dfs(board, i, j, word, 0)) return true;
        return false;
    }

    bool dfs(vector<vector<char>>& board, int x, int y, const string& word, int k) {
        if (k == word.size() - 1) return true;
        char c = board[x][y];
        board[x][y] = '#';
        bool exist = false;
        for (int i = 0; i < 4; ++i) {
            int nx = x + go[i], ny = y + go[i+1];
            if (nx < 0 || nx >= m || ny < 0 || ny >= n || board[nx][ny] != word[k+1]) continue;
            if (dfs(board, nx, ny, word, k+1)) {
                exist = true;
                break;
            }
        }
        board[x][y] = c;
        return exist;
    }
};
```
