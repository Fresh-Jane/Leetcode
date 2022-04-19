### 871. Minimum Number of Refueling Stops (Hard)

https://leetcode.com/problems/minimum-number-of-refueling-stops/

```
// Greedy
class Solution {
public:
    int minRefuelStops(int target, int startFuel, vector<vector<int>>& stations) {
        int max_dis = startFuel;
        int res = 0, i = 0;
        const int n = stations.size();
        priority_queue<int> pq;
        while(max_dis < target) {
            while(i < n && max_dis >= stations[i][0]) 
                pq.push(stations[i++][1]);
            if (pq.empty()) return -1;
            max_dis += pq.top();
            pq.pop();
            res++;
        }
        return res;
    }
};
```
