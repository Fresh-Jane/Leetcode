### 17. Letter Combinations of a Phone Number (Medium)

https://leetcode.com/problems/letter-combinations-of-a-phone-number/

```
class Solution {
public:
    vector<string> letterCombinations(string digits) {
        if (digits.empty()) return {};
        vector<string> m = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
        vector<string> res({""});
        for (auto c : digits) {
            vector<string> t;
            int d = c - '0';
            for (string r : res) 
                for (auto cc : m[d]) t.push_back(r+cc);
            res = t;
        }
        return res;
    }
};
```
