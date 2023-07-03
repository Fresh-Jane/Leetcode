### 191. Number of 1 Bits (Easy)

https://leetcode.com/problems/number-of-1-bits/description/

```
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int res = 0;
        while(n) {
            res++;
            n &= n-1;
        }
        return res;
    }
};
```
