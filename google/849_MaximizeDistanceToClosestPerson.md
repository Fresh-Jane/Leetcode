### 849. Maximize Distance to Closest Person (Medium)

https://leetcode.com/problems/maximize-distance-to-closest-person/

```
class Solution {
public:
    int maxDistToClosest(vector<int>& seats) {
        const int len = seats.size();
        int i = -1, j = 0;
        int res = 0;
        while (j < len) {
            if (seats[j] == 1) {
                res = i == -1 ? max(res, j) : max(res, (j - i) / 2);
                i = j;
            }
            ++j;
        }
        if (i != len - 1) res = max(res, len - 1 - i);
        return res;
    }
};
```
