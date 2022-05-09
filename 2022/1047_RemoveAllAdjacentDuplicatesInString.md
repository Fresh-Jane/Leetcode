### 1047. Remove All Adjacent Duplicates In String (Easy)

https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/

```
class Solution {
public:
    string removeDuplicates(string s) {
        string res;
        for (char c : s) {
            if (res.empty() || res.back() != c) res += c;
            else res.pop_back();
        }
        return res;
    }
};
```
