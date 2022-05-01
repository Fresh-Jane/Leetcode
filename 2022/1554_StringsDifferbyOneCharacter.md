### 1554. Strings Differ by One Character (Medium)

https://leetcode.com/problems/strings-differ-by-one-character/

```
class Solution {
public:
    bool differByOne(vector<string>& dict) {
        const int n = dict.size();
        if (n <= 1) return false;
        const int m = dict[0].size();
        unordered_set<string> dic_set;
        for (int i = 0; i < n; ++i) {
            string s = dict[i];
            for (int j = 0; j < m; ++j) {
                char cur = s[j];
                s[j] = '*';
                if (dic_set.count(s)) return true;
                dic_set.insert(s);
                s[j] = cur;
            }
        }
        return false;
    }
};
```
