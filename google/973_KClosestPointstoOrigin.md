### 973. K Closest Points to Origin (Medium)

https://leetcode.com/problems/k-closest-points-to-origin/

```
// Time: O(nLogk)
class Solution {
public:
    vector<vector<int>> kClosest(vector<vector<int>>& points, int k) {
        priority_queue<pair<int, int>> q;
        vector<vector<int>> res;
        for (int i = 0; i < points.size(); ++i) {
            int dis = points[i][0] * points[i][0] + points[i][1] * points[i][1];
            if (q.size() < k) q.push(make_pair(dis, i));
            else if (q.top().first > dis) {
                q.pop();
                q.push(make_pair(dis, i));
            }
        }
        while(!q.empty()) {
            res.push_back(points[q.top().second]);
            q.pop();
        }
        return res;
    }
};

// Time: O(nlogn)
class Solution {
public:
    vector<vector<int>> kClosest(vector<vector<int>>& points, int k) {
        nth_element(points.begin(), points.begin()+k, points.end(), [](vector<int>& a, vector<int>& b){
            return a[0] * a[0] + a[1] * a[1] < b[0] * b[0] + b[1] * b[1];
        });
        return vector<vector<int>>(points.begin(), points.begin()+k);
    }
};
```
