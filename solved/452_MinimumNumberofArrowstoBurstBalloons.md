### 452. Minimum Number of Arrows to Burst Balloons (Medium)

https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/description/

```
// Greedy
// 
class Solution {
public:
    int findMinArrowShots(vector<vector<int>>& points) {
        sort(points.begin(), points.end(), [](const vector<int>& p1, const vector<int>& p2){
            if (p1[0] == p2[0]) return p1[1] < p2[1];
            return p1[0] < p2[0];
        });
        long long pre_end = LONG_MIN;
        int overlap = 0;
        for (const vector<int>& p : points) {
            if (p[0] <= pre_end) {
                ++overlap;
                pre_end = min(pre_end, (long long)p[1]);
            } else pre_end = p[1];
        }
        return points.size() - overlap;
    }
};
```
