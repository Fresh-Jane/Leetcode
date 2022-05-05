### 249. Group Shifted Strings (Medium)

https://leetcode.com/problems/group-shifted-strings/

```
// Use hashmap to save string vectors with the same pattern.
// The pattern of one string is to convert it into the first char as 'a'.
class Solution {
public:
    vector<vector<string>> groupStrings(vector<string>& strings) {
        unordered_map<string, vector<string>> m;
        for (const string& s : strings) {
            int d = s[0]-'a';
            string cs = s;
            for(char& c : cs) c = c - d >= 'a' ? c-d : c+26-d;
            m[cs].push_back(s);
        }
        vector<vector<string>> res;
        for (auto p : m) res.push_back(p.second);
        return res;
    }
};
```
