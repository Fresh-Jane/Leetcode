### 14. Longest Common Prefix (Easy)

https://leetcode.com/problems/longest-common-prefix/

```
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        int l = 0;
        string res;
        while(true) {
            char cur = 0;
            for (string& s : strs) {
                if (l == s.size()) return res;
                if (!cur) cur = s[l];
                else if (cur != s[l]) return res;
            }
            if (!cur) return res;
            res += cur;
            l++;
        }
        return res;
    }
};
```
