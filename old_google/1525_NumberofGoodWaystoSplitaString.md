### 1525. Number of Good Ways to Split a String (Medium)

https://leetcode.com/problems/number-of-good-ways-to-split-a-string/

```
// solution 1:
class Solution {
public:
    int numSplits(string s) {
        int l[26] = {}, r[26] = {}, d_l = 0, d_r = 0, res = 0;
        for (const char c : s) d_r += ++r[c - 'a'] == 1;
        for (const char c : s) {
            d_l += ++l[c - 'a'] == 1;
            d_r -= --r[c - 'a'] == 0;
            res += d_l == d_r;
        }
        return res;
    }
};

// solution 2:
class Solution {
public:
    int numSplits(string s) {
        unordered_map<char, int> sum_m;
        for (const char c : s) sum_m[c]++;
        int res = 0;
        unordered_set<char> pre_s;
        for (const char c : s) {
            pre_s.insert(c);
            sum_m[c]--;
            if (!sum_m[c]) sum_m.erase(c);
            if (sum_m.size() == pre_s.size()) res++;
        }
        return res;
    }
};
```
