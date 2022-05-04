### 1249. Minimum Remove to Make Valid Parentheses (Medium)

https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/

```
class Solution {
public:
    string minRemoveToMakeValid(string s) {
        deque<int> q;
        for (int i = 0; i < s.size(); ++i) {
            if (s[i] == '(') q.push_back(i);
            else if (s[i] == ')') {
                if (q.empty()) s[i] = '*';
                else q.pop_back();
            }
        }
        string res;
        for (int i = 0; i < s.size(); ++i) {
            if (!q.empty() && i == q.front()) {
                q.pop_front();
                continue;
            }
            if (s[i] == '*') continue;
            res += s[i];
        }
        return res;
    }
};
```
