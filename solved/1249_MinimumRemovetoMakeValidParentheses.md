### 1249. Minimum Remove to Make Valid Parentheses (Medium)

https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/

```
class Solution {
public:
    string minRemoveToMakeValid(string s) {
        vector<int> left;
        string res;
        for (int i = 0; i < s.size(); ++i) {
            if (s[i] == '(') left.push_back(res.size());
            else if (s[i] == ')') {
                if (!left.empty()) left.pop_back();
                else continue;
            }
            res += s[i];
        }
        int del = 0;
        for (int pos : left) {
            res.erase(res.begin()+pos-del);
            del++;
        }
        return res;
    }
};

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
