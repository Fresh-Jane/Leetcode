### 1304. Find N Unique Integers Sum up to Zero (Easy)

https://leetcode.com/problems/find-n-unique-integers-sum-up-to-zero/

```
class Solution {
public:
    vector<int> sumZero(int n) {
        vector<int> res;
        res.reserve(n);
        for (int i = 1; i <= n/2; ++i) {
            res.push_back(i);
            res.push_back(-i);
        }
        if (n % 2) res.push_back(0);
        return res;
    }
};
```
