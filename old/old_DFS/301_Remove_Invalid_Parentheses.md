### 301. Remove Invalid Parentheses (Hard)

Remove the minimum number of invalid parentheses in order to make the input string valid. Return all possible results.

Note: The input string may contain letters other than the parentheses ( and ).

Example 1:

```
Input: "()())()"
Output: ["()()()", "(())()"]
```
Example 2:

```
Input: "(a)())()"
Output: ["(a)()()", "(a())()"]
```
Example 3:

```
Input: ")("
Output: [""]
```
```

// DFS 2
class Solution 2 {
public:
    void dfs(string s, string cur, int cur_iter, 
             unordered_set<string>& res, int fl, int fr, int pairs) {
        if (cur_iter == (int)s.size()) {
            if (!fl && !fr && !pairs) res.insert(cur);
            return;
        }
        char c = s[cur_iter];
        if (s[cur_iter] == '(') {
            if (fl > 0)  dfs(s, cur, cur_iter+1, res, fl-1, fr, pairs);
            dfs(s, cur+c, cur_iter+1, res, fl, fr, pairs+1);
        }
        else if (s[cur_iter] == ')'){
            if (fr > 0) dfs(s, cur, cur_iter+1, res, fl, fr-1, pairs);
            if (pairs > 0) dfs(s, cur+c, cur_iter+1, res, fl, fr, pairs-1);
        }
        else {
            dfs(s, cur+c, cur_iter+1, res, fl, fr, pairs);
        }
    }
    
    vector<string> removeInvalidParentheses(string s) {
        int fl = 0, fr = 0;
        for (const char c : s) {
            if (c == '(') fl++;
            else if (c == ')') {
                if (!fl) fr++;
                else fl--;
            }
        }
        unordered_set<string> res;
        dfs(s, "", 0, res, fl, fr, 0);
        return vector<string>(res.begin(), res.end());
    }
};


// DFS 3
class Solution 3 {
public:
    bool isValid(string s) {
        int fl = 0;
        for (const char c : s) {
            if (c == '(') fl++;
            else if (c == ')') {
                if (!fl) return false;
                else fl--;
            }
        }
        return !fl;
    } 
    
    void dfs(string s, string cur, int cur_iter, 
             unordered_set<string>& res, int fl, int fr) {
        if (!fl && !fr) {
            cur += s.substr(cur_iter);
            if (isValid(cur)) res.insert(cur);
            return;
        }
        if (cur_iter == s.size()) return;
        dfs(s, cur+s[cur_iter], cur_iter+1, res, fl, fr);
        if (s[cur_iter] == '(' && fl) 
            dfs(s, cur, cur_iter+1, res, fl-1, fr);
        else if (s[cur_iter] == ')' && fr)
            dfs(s, cur, cur_iter+1, res, fl, fr-1);
    }
    
    vector<string> removeInvalidParentheses(string s) {
        int fl = 0, fr = 0;
        for (const char c : s) {
            if (c == '(') fl++;
            else if (c == ')') {
                if (!fl) fr++;
                else fl--;
            }
        }
        unordered_set<string> r;
        dfs(s, "", 0, r, fl, fr);
        vector<string> res;
        for (const string one_r : r) res.push_back(one_r);
        return res;
    }
};
```
