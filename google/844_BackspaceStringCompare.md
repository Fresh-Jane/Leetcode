### 844. Backspace String Compare (Easy)

https://leetcode.com/problems/backspace-string-compare/

```
// Time: O(N), Space: O(N)
class Solution {
public:
    string getBackspace(string s) {
        string res;
        for (const auto c : s) {
            if (c != '#') res += c;
            else if (res != "") res.pop_back();
        }
        return res;
    }
    bool backspaceCompare(string s, string t) {
        return getBackspace(s) == getBackspace(t);
    }
};

// Time: O(N), Space: O(1)
class Solution {
public:
    bool backspaceCompare(string s, string t) {
        int i = s.size() - 1, j = t.size() - 1, back;
        while(true) {
            back = 0;
            while(i >= 0 && (back > 0 || s[i] == '#')) {
                back += s[i] == '#' ? 1 : -1;
                --i;
            }
            back = 0;
            while(j >= 0 && (back > 0 || t[j] == '#')) {
                back += t[j] == '#' ? 1 : -1;
                --j;
            }
            if (i >= 0 && j >= 0 && s[i] == t[j]) {
                --i;
                --j;
            } else {
                break;
            }
        }
        return i == -1 && j == -1;
    }
};
```
