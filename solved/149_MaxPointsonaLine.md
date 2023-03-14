### 149. Max Points on a Line (Hard)

https://leetcode.com/problems/max-points-on-a-line/

```
// We simplify the problem and search the maximum number of points passing through the point i.
// And we only need to focus on the following points, the points with smaller index have been processed.
// Since we are drawing the lines between start point i and each of the following points, if they share the same slope, they are on the same line.  
class Solution {
public:
    int maxPoints(vector<vector<int>>& points) {
        constexpr double kMax = numeric_limits<double>::max();
        const int n = points.size();
        int res = 1;
        for (int i = 0; i < n; ++i) {
            const int x0 = points[i][0], y0 = points[i][1];
            unordered_map<double, int> lines;
            for (int j = i+1; j < n; ++j) {
                const int x1 = points[j][0], y1 = points[j][1];
                double slop;
                if (x1 == x0) slop = kMax;
                else slop = (y1 - y0) * 1.0 / (x1 - x0);
                ++lines[slop];
            }
            for (auto line : lines) res = max(res, line.second + 1);
        }
        return res;
    }
};
```
