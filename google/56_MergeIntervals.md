### 56. Merge Intervals (Medium)

https://leetcode.com/problems/merge-intervals/

```
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        const int len = intervals.size();
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> res;
        int l = intervals[0][0], r = intervals[0][1];
        for (int i = 1; i < len; ++i) {
            const int cl = intervals[i][0], cr = intervals[i][1];
            if (r < cl) {
                res.push_back({l, r});
                l = cl;
                r = cr;
            } else {
                r = std::max(r, cr);
            }
        }
        res.push_back({l, r});
        return res;
    }
};
```
