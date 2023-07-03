### 1732. Find the Highest Altitude (Easy)

https://leetcode.com/problems/find-the-highest-altitude/description/

```
class Solution {
public:
    int largestAltitude(vector<int>& gain) {
        int res = 0, sum = 0;
        for (int g : gain) {
            sum += g;
            res = max(res, sum);
        }
        return res;
    }
};
```
