### 49. Group Anagrams (Medium)

https://leetcode.com/problems/group-anagrams

```
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> m;
        for(string& s : strs) {
            string cur = s;
            sort(cur.begin(), cur.end());
            m[cur].push_back(s);
        }
        vector<vector<string>> res;
        for (const auto& s_pair : m) res.push_back(s_pair.second);
        return res;
    }
};
```
