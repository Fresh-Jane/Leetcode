### 849. Maximize Distance to Closest Person (Medium)

https://leetcode.com/problems/maximize-distance-to-closest-person/

```
class Solution {
public:
    int maxDistToClosest(vector<int>& seats) {
        int n = seats.size();
        int res = 0, last = -1;
        for (int i = 0; i < n; ++i) {
            if (seats[i]) {
                res = last == -1 ? i : max(res, (i-last)/2);
                last = i;
            }
        }
        res = max(res, n-1-last);
        return res;
    }
};
```
