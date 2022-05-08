### 1891. Cutting Ribbons (Medium)

https://leetcode.com/problems/cutting-ribbons/

```
class Solution {
public:
    int maxLength(vector<int>& ribbons, int k) {
        int max_v = INT_MIN;
        for (int r : ribbons) max_v = max(max_v, r);
        int l = 1, r = max_v;
        while(l <= r) {
            int m = l + (r - l) / 2;
            if (can_reach(ribbons, m, k)) l = m + 1;
            else r = m-1;
        }
        return r;
    }
    bool can_reach(vector<int>& ribbons, int num, int k) {
        int n = 0;
        for (int r : ribbons) {
            n += r / num;
            if (n >= k) return true;
        }
        return false;
    }
};
```
