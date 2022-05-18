### 1578. Minimum Time to Make Rope Colorful (Medium)

https://leetcode.com/problems/minimum-time-to-make-rope-colorful/

```
class Solution {
public:
    int minCost(string colors, vector<int>& neededTime) {
        int max_t = 0, sum_t = 0, res = 0;
        for (int i = 0; i < colors.size(); ++i) {
            if (i > 0 && colors[i] != colors[i-1]) {
                res += sum_t - max_t;
                max_t = sum_t = 0;
            }
            max_t = max(max_t, neededTime[i]);
            sum_t += neededTime[i];
        }
        res += sum_t - max_t;
        return res;
    }
};
```
