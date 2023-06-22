### 784. Letter Case Permutation (Medium)

https://leetcode.com/problems/letter-case-permutation/description/

```
// DFS
class Solution {
public:
    vector<string> letterCasePermutation(string s) {
        vector<string> res;
        dfs(s, 0, res);
        return res;
    }
    void dfs(string& s, int index, vector<string>& res) {
        if (index == s.size()) {
            res.push_back(s);
            return;
        }
        dfs(s, index+1, res);
        char c = s[index];
        if (islower(c)) { // can learn the if the char is a lowercase
            s[index] = toupper(c);
            dfs(s, index+1, res);
        } else if (isupper(c)) {
            s[index] = tolower(c);
            dfs(s, index+1, res);
        }
        s[index] = c;
    }
};
```
