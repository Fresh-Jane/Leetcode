### 126. Word Ladder II (Hard)

https://leetcode.com/problems/word-ladder-ii/description/

```
// step1: use BFS to construct the transaction tree from beginWord to endWord
// step2: use DFS from end word to search and save all valid path to begin word
// We don't search from begin word because from end word we can filter many unvalid path.

class Solution {
public:
    vector<vector<string>> res;
    vector<string> path;
    unordered_map<string, int> tree;
    string b;
    void dfs(string s) {
        path.push_back(s);
        if (s == b) {
            vector<string> x = path;
            reverse(x.begin(), x.end());
            res.push_back(x);
            path.pop_back();
            return;
        }
        int level = tree[s];
        for (int i = 0; i < s.size(); ++i) {
            char c = s[i];
            for (char cc = 'a'; cc <= 'z'; ++cc) {
                s[i] = cc;
                if (tree.count(s) && tree[s] == level - 1) dfs(s);
            }
            s[i] = c;
        }
        path.pop_back();
    }

    vector<vector<string>> findLadders(string beginWord, string endWord, vector<string>& wordList) {
        for (const string& w : wordList) tree[w] = -1;
        if (!tree.count(endWord)) return {};
        queue<string> q;
        q.push(beginWord);
        int level = 0;
        tree[beginWord] = 0;
        b = beginWord;
        int k = beginWord.size();
        while(!q.empty()) {
            int len = q.size();
            while(len--) {
                string cur = q.front(); q.pop();
                for (int i = 0; i < k; ++i) {
                    for (char c = 'a'; c <= 'z'; ++c) {
                        string now = cur;
                        now[i] = c;
                        if (tree.count(now) && tree[now] == -1) {
                            q.push(now);
                            tree[now] = level + 1;
                        }
                    }
                }
            }
            level++;
        }
        dfs(endWord);
        return res;
    }
};
```
