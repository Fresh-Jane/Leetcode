### 8. String to Integer (atoi) (Medium)

https://leetcode.com/problems/string-to-integer-atoi/description/

```
class Solution {
public:
    int myAtoi(string s) {
        if (s.empty()) return 0;
        const int n = s.size();
        int i = 0, sign = 1;
        while (s[i] == ' ') ++i;
        if (s[i] == '+') ++i;
        else if (s[i] == '-') {
            sign = -1; 
            ++i;
        }
        int res = 0;
        for (; i < n; ++i) {
            if (s[i] < '0' || s[i] > '9') break;
            if (res > INT_MAX / 10 ||
                (res == INT_MAX / 10 && s[i]-'0' > INT_MAX % 10)) {
                return sign == 1 ? INT_MAX : INT_MIN;
            }
            res = res * 10 + (s[i] - '0');
        }
        return sign * res;
    }
};
```
