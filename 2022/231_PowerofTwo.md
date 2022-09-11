### 231. Power of Two (Easy)

https://leetcode.com/problems/power-of-two/

```
// bit manipulation
class Solution {
public:
    bool isPowerOfTwo(int n) {
        return (n > 0) && ((n&(n-1)) == 0);
    }
};

// Recursive 
class Solution {
public:
    bool isPowerOfTwo(int n) {
        if (n <= 0) return false;
        if (n == 1) return true;
        if (n % 2) return false;
        return isPowerOfTwo(n/2);
    }
};
```
