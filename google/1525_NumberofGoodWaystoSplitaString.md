### 1525. Number of Good Ways to Split a String (Medium)

https://leetcode.com/problems/number-of-good-ways-to-split-a-string/

```
class Solution {
public:
    int numSplits(string s) {
        int l[26] = {}, r[26] = {}, d_l = 0, d_r = 0, res = 0;
        for (const char c : s) d_r += ++r[c - 'a'] == 1;
        for (int i = 0; i < s.size(); ++i) {
            d_l += ++l[s[i] - 'a'] == 1;
            d_r -= --r[s[i] - 'a'] == 0;
            res += d_l == d_r;
        }
        return res;
    }
};
```
