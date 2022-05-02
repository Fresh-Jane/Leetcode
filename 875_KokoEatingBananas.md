### 875. Koko Eating Bananas (Medium)

https://leetcode.com/problems/koko-eating-bananas/

```
// Binary search
// The search range is the [ave_p, max_p], the can function show if each situation is valid.
class Solution {
public:
    int minEatingSpeed(vector<int>& piles, int h) {
        int max_p = 0;
        long long ave_p = 0;
        for (int p : piles) {
            max_p = max(max_p, p);
            ave_p += p;
        }
        ave_p /= h;
        int l = ave_p, r = max_p;
        while(l < r) {
            int m = l + (r - l) / 2;
            if (can(piles, m, h)) r = m;
            else l = m+1;
        }
        return r;
    }
    bool can(vector<int>& piles, int k, int h) {
        if (k == 0) return false;
        for (int p : piles) {
            h -= (p-1)/k+1;
            if (h < 0) return false;
        }
        return true;
    }
};
```
