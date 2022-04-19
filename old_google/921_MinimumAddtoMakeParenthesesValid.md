### 921. Minimum Add to Make Parentheses Valid (Medium)

https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/

```
// Time: O(n)
// Space: O(1)
class Solution {
public:
    int minAddToMakeValid(string s) {
        int res = 0, left_num = 0;
        for (const char c : s) {
            if (c == '(') ++left_num;
            else {
                if (left_num) --left_num;
                else ++res;
            }
        }
        return res + left_num;
    }
};
```
