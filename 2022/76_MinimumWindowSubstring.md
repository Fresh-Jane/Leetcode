### 76. Minimum Window Substring (Hard)

https://leetcode.com/problems/minimum-window-substring/

```
// Sliding window
class Solution {
public:
    string minWindow(string s, string t) {
        vector<int> tm(128, 0);
        for (auto c : t) ++tm[c];
        const int n = s.size();
        int l = 0, r = 0, tn = t.size();
        int start = 0, len = INT_MAX;
        while(r < n) {
            // no matter the result of condition is true or false, the r++ and tm[]-- will execute.
            // this condition is before the ++ and --.
            if (tm[s[r++]]-- > 0) tn--; 
            while (tn == 0) {
                if (r - l < len) {
                    start = l; 
                    len = r - l;
                }
                if (tm[s[l++]]++ == 0) tn++;
            }
        }
        return len == INT_MAX ? "" : s.substr(start, len);
    }
};
```
