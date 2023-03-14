### 76. Minimum Window Substring (Hard)

https://leetcode.com/problems/minimum-window-substring/

```
// Sliding window
// The question asks us to return the minimum window from the string S to contain all characters in string t.
// We can use a simple sliding window approach to solve this problem.
// In general, we have two pointers in sliding window. One right pointer to expand the window and left one to contract the window.
// We expand the right pointer to contain more characters, when all t characters are int the window, we start to move left one to contract the window.
// The time complexity is O(S+T). 
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
