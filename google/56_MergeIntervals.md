### 56. Merge Intervals (Medium)

https://leetcode.com/problems/merge-intervals/

```
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end(), 
             [](const vector<int>& a, const vector<int>& b) {
                return a[0] < b[0];
             });
        vector<vector<int>> res;
        for (const vector<int>& interval : intervals) {
            if (res.empty() || interval[0] > res.back()[1]) {
                res.push_back(interval);
            } else if (interval[0] <= res.back()[1]) {
                res.back()[1] = max(res.back()[1], interval[1]);
            }
        }
        return res;
    }
};
```
