### 50. Pow(x, n) (Medium)

https://leetcode.com/problems/powx-n/

```
class Solution {
public:
    double myPow(double x, int n) {
        if (n < 0) {
            if (n == INT_MIN) return myPow(x, n/2) * myPow(x, n/2);
            else return 1.0 / myPow(x, -n);
        }
        double res = 1;
        while(n) {
            if(n&1) res *= x;
            x *= x;
            n >>= 1;
        }
        return res;
    }
};
```
