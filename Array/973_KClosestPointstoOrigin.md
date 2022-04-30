### 973. K Closest Points to Origin (Medium)

https://leetcode.com/problems/k-closest-points-to-origin/

```
class Solution {
public:
    vector<vector<int>> kClosest(vector<vector<int>>& points, int k) {
        const int n = points.size();
        vector<int> dis(n, 0);
        for (int i = 0; i < n; ++i) {
            const vector<int>& p = points[i];
            dis[i] = p[0]*p[0] + p[1]*p[1];
        }
        auto cmp = [&dis](int i, int j) {
            return dis[i] < dis[j];
        };
        priority_queue<int, vector<int>, decltype(cmp)> pq(cmp);
        for (int i = 0; i < n; ++i) {
            pq.push(i);
            if (pq.size() > k) pq.pop();
        }
        vector<vector<int>> res;
        while(!pq.empty()) {
            res.push_back(points[pq.top()]);
            pq.pop();
        }
        return res;
    }
};
```
