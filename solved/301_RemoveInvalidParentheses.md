### 301. Remove Invalid Parentheses (Hard)

https://leetcode.com/problems/remove-invalid-parentheses/description/

```
// DFS
class Solution {
public:
    unordered_set<string> res_set;
    vector<string> removeInvalidParentheses(string s) {
        int lefts = 0, rights = 0;
        for (char c : s) {
            if (c == '(') ++lefts;
            else if (c == ')') {
                if (lefts > 0) --lefts;
                else ++rights;
            }
        }
        string path;
        dfs(s, 0, lefts, rights, 0, path);
        return vector<string>(res_set.begin(), res_set.end());
    }
    void dfs(const string& s, int start, int lefts, int rights, int pairs, string& path) {
        if (start == s.size()) {
            if (lefts == 0 && rights == 0 && pairs == 0) res_set.insert(path);
            return;
        }
        char c = s[start];
        if (c == '(') {
            if (lefts > 0) dfs(s, start+1, lefts-1, rights, pairs, path);
            path += c;
            dfs(s, start+1, lefts, rights, pairs+1, path);
            path.pop_back();
        } else if (c == ')') {
            if (rights > 0) dfs(s, start+1, lefts, rights-1, pairs, path);
            if (pairs > 0) {
                path += c;
                dfs(s, start+1, lefts, rights, pairs-1, path);
                path.pop_back();
            }
        } else {
            path += c;
            dfs(s, start+1, lefts, rights, pairs, path);
            path.pop_back();
        }
    }
};

```
