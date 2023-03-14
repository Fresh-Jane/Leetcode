### 696. Count Binary Substrings (Easy)

https://leetcode.com/problems/count-binary-substrings/

```
class Solution {
public:
    int countBinarySubstrings(string s) {
        int res = 0;
        int preLen = 0, curLen = 1;
        for (int i = 1; i < s.size(); ++i) {
            if (s[i] == s[i-1]) ++curLen;
            else {
                preLen = curLen;
                curLen = 1;
            }
            if (preLen >= curLen) ++res;
        }
        return res;
    }
};
```
