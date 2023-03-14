### 342. Power of Four (Easy)

https://leetcode.com/problems/power-of-four/

```
// Solution 1: Math
class Solution {
public:
    bool isPowerOfFour(int n) {
        if (n <= 0) return false;
        if (n & (n-1)) return false;
        return (n - 1) % 3 == 0;
    }
};

// Solution 2: Recursive
class Solution {
public:
    bool isPowerOfFour(int n) {
        if (n <= 0) return false;
        if (n == 1) return true;
        if (n % 4) return false;
        return isPowerOfFour(n/4);
    }
};
```
