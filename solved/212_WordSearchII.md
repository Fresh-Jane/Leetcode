### 212. Word Search II (Hard)

https://leetcode.com/problems/word-search-ii/description/

```
// First we should construct the word tree to save some prefix
class Solution {
public:
    struct Node {
        bool is_end;
        Node* next[26];
    };
    Node* root;
    void insertWord(const string& w) {
        Node* cur = root;
        for (char c : w) {
            int t = c - 'a';
            if (!cur->next[t]) cur->next[t] = new Node();
            cur = cur->next[t];
        }
        cur->is_end = true;
    }

    int m, n;
    vector<int> go = {1, 0, -1, 0, 1};
    unordered_set<string> res;
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        if (board.empty() || words.empty()) return {};
        root = new Node();
        for (const string& w : words) insertWord(w);

        m = board.size(); n = board[0].size();
        for (int i = 0; i < m; ++i) 
            for (int j = 0; j < n; ++j) {
                string path;
                dfs(board, i, j, path, root);   
            }
                 
        return vector<string>(res.begin(), res.end());
    }
    void dfs(vector<vector<char>>& board, int x, int y, string& path, Node* cur) {
        char c = board[x][y];
        int t = c - 'a';
        if (cur->next[t] == nullptr) return;
        cur = cur->next[t];
        path += c;
        if (cur->is_end) res.insert(path);
        board[x][y] = '#';
        for (int i = 0; i < 4; ++i) {
            int nx = x + go[i], ny = y + go[i+1];
            if (nx < 0 || nx >= m || ny < 0 || ny >= n || board[nx][ny] == '#') continue;
            dfs(board, nx, ny, path, cur);
        }
        path.pop_back();
        board[x][y] = c;
    }
};
```
