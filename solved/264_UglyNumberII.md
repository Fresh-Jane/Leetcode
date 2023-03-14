### 264. Ugly Number II (Medium)

https://leetcode.com/problems/ugly-number-ii/

```
// Use one vector to record the first nth Ugly number.
// Use three index to record the smallest index of number generated using the certain prime factor and the initial is 0.
class Solution {
public:
    int nthUglyNumber(int n) {
        vector<int> res(n, 1);
        int p2 = 0, p3 = 0, p5 = 0;
        for (int i = 1; i < n; ++i) {
            int r2 = res[p2] * 2, r3 = res[p3] * 3, r5 = res[p5] * 5;
            res[i] = min(r2, min(r3, r5));
            if (res[i] == r2) ++p2;
            if (res[i] == r3) ++p3;
            if (res[i] == r5) ++p5;
        }
        return res[n-1];
    }
};
```
