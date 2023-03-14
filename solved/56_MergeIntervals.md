### 56. Merge Intervals (Medium)

https://leetcode.com/problems/merge-intervals/

```
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        vector<vector<int>> res;
        if (intervals.empty()) return res;
        sort(intervals.begin(), intervals.end(),
            [](const vector<int>& i1, const vector<int>& i2){
                if(i1[0] == i2[0]) return i1[1] < i2[1];
                return i1[0] < i2[0];
            });
        for (int i = 0; i < intervals.size(); ++i) {
            if (i == 0 || intervals[i][0] > res.back()[1]) res.push_back(intervals[i]);
            else res.back()[1] = max(res.back()[1], intervals[i][1]);
        }
        return res;
    }
};
```
