### 967. Numbers With Same Consecutive Differences (Medium)

https://leetcode.com/problems/numbers-with-same-consecutive-differences/

```
class Solution {
public:
    vector<int> res;
    vector<int> numsSameConsecDiff(int n, int k) {
        for (int i = 1; i <= 9; ++i) dfs(n-1, k, i, 0);
        return res;
    }
    void dfs(int n, int k, int i, int num) {
        num = 10 * num + i;
        if (n == 0) {
            res.push_back(num);
            return;
        }
        if (i + k <= 9) dfs(n-1, k, i+k, num);
        if (i - k >= 0 && k != 0) dfs(n-1, k, i-k, num);
    }
};
```
