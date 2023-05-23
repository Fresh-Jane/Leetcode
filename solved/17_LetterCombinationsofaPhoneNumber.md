### 17. Letter Combinations of a Phone Number (Medium)

https://leetcode.com/problems/letter-combinations-of-a-phone-number/

```
class Solution {
public:
    vector<string> letterCombinations(string digits) {
        if (digits.empty()) return {};
        vector<string> m = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
        vector<string> res({""});
        for (const char c : digits) {
            vector<string> t;
            const int d = c - '0';
            for (const string& r : res) 
                for (const char cc : m.at(d)) t.push_back(r+cc);
            res = t;
        }
        return res;
    }
};
```
