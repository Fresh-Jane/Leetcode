### 921. Minimum Add to Make Parentheses Valid (Medium)

https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/

```
// The valid opening parenthesis must occur before the closing parenthesis.
// So ln records the non-matching opening parenthesis and rn records the number of closing parenthesis before the opening one.
class Solution {
public:
    int minAddToMakeValid(string s) {
        int ln = 0, rn = 0;
        for (int i = 0; i < s.size(); ++i) {
            if (s[i] == '(') ln++;
            else {
                if (ln) ln--;
                else rn++;
            }
        }
        return ln + rn;
    }
};
```
