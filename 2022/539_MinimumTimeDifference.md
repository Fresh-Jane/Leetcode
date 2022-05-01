### 539. Minimum Time Difference (Medium)

https://leetcode.com/problems/minimum-time-difference/

```
class Solution {
public:
    int findMinDifference(vector<string>& timePoints) {
        vector<int> time;
        for (const string& t : timePoints) 
            time.push_back(stoi(t.substr(0, 2))*60 + stoi(t.substr(3, 2)));
        sort(time.begin(), time.end());
        time.push_back(time[0] + 24*60);
        int res = INT_MAX;
        for (int i = 1; i < time.size(); ++i) 
            res = min(res, time[i] - time[i-1]);
        return res;
    }
};
```
