### 205. Isomorphic Strings (Easy)

https://leetcode.com/problems/isomorphic-strings/

```
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        if (s.empty() && t.empty()) return true;
        if (s.size() != t.size()) return false;
        vector<int> ms(128, 0), mt(128, 0);
        for (int i = 0; i < s.size(); ++i) {
            if (ms[s[i]] != mt[t[i]]) return false;
            ms[s[i]] = mt[t[i]] = i + 1;
        }
        return true;
    }
};
```
