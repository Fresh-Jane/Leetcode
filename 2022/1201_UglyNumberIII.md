### 1201. Ugly Number III (Medium)

https://leetcode.com/problems/ugly-number-iii/

```
// https://leetcode.com/problems/ugly-number-iii/discuss/387539/cpp-Binary-Search-with-picture-and-Binary-Search-Template
class Solution {
public:
    int nthUglyNumber(int n, int a, int b, int c) {
        int lo = 1, hi = 2 * (int)1e9;
        long la = (long)a, lb = (long)b, lc = (long)c;
        long ab = la * lb / __gcd(la, lb);
        long ac = la * lc / __gcd(la, lc);
        long bc = lb * lc / __gcd(lb, lc);
        long abc = la * bc / __gcd(la, bc);
        while(lo < hi) {
            int mid = lo + (hi - lo) / 2;
            int k = mid / la + mid / lb + mid / lc - mid / ab - mid / bc - mid / ac + mid / abc;
            if (k < n) lo = mid + 1;
            else hi = mid;
        }
        return lo;
    }
};
```
