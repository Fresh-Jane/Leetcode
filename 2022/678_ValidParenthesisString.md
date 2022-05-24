### 678. Valid Parenthesis String (Medium)

https://leetcode.com/problems/valid-parenthesis-string/

```
// Count the possible open parenthesis number.
class Solution {
public:
    bool checkValidString(string s) {
        int lo = 0, hi = 0;
        for (char c : s) {
            lo += c == '(' ? 1 : -1;
            hi += c != ')' ? 1 : -1;
            if (hi < 0) break;
            lo = max(lo, 0);
        }
        return lo == 0;
    }
};
```
