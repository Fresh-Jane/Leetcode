### 65. Valid Number (Hard)

https://leetcode.com/problems/valid-number/

```
// https://leetcode.com/problems/valid-number/solution/
// Check all invalid situations
class Solution {
public:
    bool isNumber(string s) {
        bool seenDigit = false, seenDot = false, seenExponent = false;
        for (int i = 0; i < s.size(); ++i) {
            if (isdigit(s[i])) {
                seenDigit = true;
            } else if (s[i] == '.') {
                if (seenDot || seenExponent) return false;
                seenDot = true;
            } else if (s[i] == 'e' || s[i] == 'E') {
                if (seenExponent || !seenDigit) return false;
                seenExponent = true;
                seenDigit = false;
            } else if (s[i] == '+' || s[i] == '-') {
                if (i != 0 && s[i-1] != 'e' && s[i-1] != 'E') return false;
            } else return false;
        }
        return seenDigit;
    }
};
```
