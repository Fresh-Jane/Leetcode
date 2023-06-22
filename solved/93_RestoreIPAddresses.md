### 93. Restore IP Addresses (Medium)

https://leetcode.com/problems/restore-ip-addresses/description/

```
class Solution {
public:
    vector<string> restoreIpAddresses(string s) {
        if (s.size() <= 3) return {};
        vector<string> res;
        vector<string> path;
        dfs(s, 0, path, res);
        return res;
    }
    void dfs(const string& s, int start, vector<string>& path, vector<string>& res) {
        if (path.size() == 4) {
            if (start == s.size()) {
                string str = path[0];
                for (int i = 1; i < 4; ++i) str += '.' + path[i];
                res.push_back(str);
            }
            return;
        }
        for (int i = start; i < s.size(); ++i) {
            if (i > start && s[start] == '0') return;
            const string num = s.substr(start, i - start + 1);
            if (stoi(num) > 255) return;
            path.push_back(num);
            dfs(s, i + 1, path, res);
            path.pop_back();
        }
    }
};
```
