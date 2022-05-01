### 1218. Longest Arithmetic Subsequence of Given Difference (Medium)

https://leetcode.com/problems/longest-arithmetic-subsequence-of-given-difference/

```
// DP
class Solution {
public:
    int longestSubsequence(vector<int>& arr, int diff) {
        unordered_map<int, int> m;
        int res = 1;
        for (auto i : arr) res = max(res, m[i] = max(m[i], 1+m[i-diff]));
        return res;
    }
};
```
