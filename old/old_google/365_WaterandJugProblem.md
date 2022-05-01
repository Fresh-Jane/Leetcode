### 365. Water and Jug Problem (Medium)

https://leetcode.com/problems/water-and-jug-problem/

```
// https://github.com/Vesion/Misirlou/blob/master/leetcode/365-WaterAndJugProblem.cpp
class Solution {
public:
    using ll = long long;
    bool canMeasureWater(ll jug1, ll jug2, ll target) {
        if (target == 0) return true;
        if (jug1 * jug2 == 0) return target == jug1 || target == jug2;
        ll g = gcd(jug1, jug2);
        return target % g == 0 && target <= jug1 + jug2;
    }
    ll gcd(ll x, ll y) {
        if (y == 0) return x;
        return gcd(y, x % y);
    } 
};
```
