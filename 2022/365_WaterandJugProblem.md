### 365. Water and Jug Problem (Medium)

https://leetcode.com/problems/water-and-jug-problem/

```
// If d is the gcd of x and y, it can be represented as d = ax+by and a,b are integer.
// If z = k * d, it should be calculated as z = k * (ax + by) and can be measured.
class Solution {
public:
    bool canMeasureWater(int x, int y, int z) {
        if (z == 0) return true;
        if ((long long)x * y == 0) return z == x || z == y;
        int d = gcd(x, y);
        return z % d == 0 && z <= x + y;
    }
    int gcd(int x, int y) {
        if (y == 0) return x;
        return gcd(y, x % y);
    }
};
```
