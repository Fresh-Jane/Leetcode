### 791. Custom Sort String (Medium)

https://leetcode.com/problems/custom-sort-string/

```
class Solution {
public:
    string customSortString(string order, string s) {
        int m[26] = {};
        for(char c : s) ++m[c-'a'];
        string res;
        for(char oc : order) {
            res += string(m[oc-'a'], oc);
            m[oc-'a'] = 0;  
        }
        for(int i = 0; i < 26; ++i) res += string(m[i], i+'a');
        return res;
    }
};
```
