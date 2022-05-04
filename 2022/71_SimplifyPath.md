### 71. Simplify Path (Medium)

https://leetcode.com/problems/simplify-path/

```
class Solution {
public:
    string simplifyPath(string path) {
        vector<string> dir;
        istringstream in(path);
        string s;
        while(getline(in, s, '/')) {
            if (s.empty() || s == ".") continue;
            if (s == "..") {
                if (!dir.empty()) dir.pop_back();
            }
            else dir.push_back(s);
        }
        if (dir.empty()) return "/";
        string res;
        for (string& file : dir) res += "/" + file;
        return res;
    }
};
```
