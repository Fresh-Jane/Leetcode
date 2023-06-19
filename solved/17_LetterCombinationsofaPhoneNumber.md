### 17. Letter Combinations of a Phone Number (Medium)

https://leetcode.com/problems/letter-combinations-of-a-phone-number/

```
class Solution {
public:
    vector<string> letterCombinations(string digits) {
        if (digits.empty()) return {};
        vector<string> m = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
        vector<string> res({""});
        for (const char c : digits) {
            vector<string> t;
            const int d = c - '0';
            for (const string& r : res) 
                for (const char cc : m.at(d)) t.push_back(r+cc);
            res = t;
        }
        return res;
    }
};

// DFS
class Solution {
public:
    vector<string> letterCombinations(string digits) {
        vector<string> res;
        if (digits.empty()) return res;
        string path;
        dfs(digits, 0, path, res);
        return res;
    }
    vector<string> charm = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    void dfs(const string& digits, int index, const string& path, vector<string>& res) {
        if (index == digits.size()) {
            res.push_back(path);
            return;
        }
        const string& chars = charm[digits[index]-'0'];
        for (const char c : chars) dfs(digits, index+1, path+c, res);
    }
};
```
