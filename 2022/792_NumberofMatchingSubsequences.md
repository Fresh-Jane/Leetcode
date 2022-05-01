### 792. Number of Matching Subsequences (Medium)

https://leetcode.com/problems/number-of-matching-subsequences/

```
class Solution {
public:
    int numMatchingSubseq(string s, vector<string>& words) {
        unordered_map<char, vector<int>> m;
        for (int i = 0; i < s.size(); ++i) m[s[i]].push_back(i);
        int res = 0;
        for (const string& w : words) if (isSub(w, m)) res++;
        return res;   
    }
    bool isSub(const string& w, unordered_map<char, vector<int>>& m) {
        int index = -1;
        for (int i = 0; i < w.size(); ++i) {
            const char c = w[i];
            if (!m.count(c)) return false;
            auto it = upper_bound(m[c].begin(), m[c].end(), index);
            if (it == m[c].end()) return false;
            index = *it;
        }
        return true;
    }
};
```
