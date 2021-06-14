### 79. Word Search (Medium)

https://leetcode.com/problems/word-search/

```
class Solution {
public:
    int m, n;
    int go[4][2] = {{0, 1}, {0, -1}, {-1, 0}, {1, 0}};
    bool dfs(const string& word, vector<vector<char>>& board, int x, int y, int w) {
        if (w == (int)word.size()-1) return true;
        const char c = board[x][y]; 
        board[x][y] = '#';
        bool res = false;
        for (const auto g : go) {
            const int nx = x + g[0];
            const int ny = y + g[1];
            if (nx < 0 || nx >= m || ny < 0 || ny >= n || board[nx][ny] != word[w+1]) continue;
            if (dfs(word, board, nx, ny, w+1)) { res = true; break; }
        }
        board[x][y] = c;
        return res;
    }
    
    bool exist(vector<vector<char>>& board, string word) {
        if (board.empty() || word.empty()) return false;
        m = board.size();
        n = board[0].size();
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) 
                if (board[i][j] == word[0] && dfs(word, board, i, j, 0)) return true;
        return false;
    }
};
```
