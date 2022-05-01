### 1834. Single-Threaded CPU (Medium)

https://leetcode.com/problems/single-threaded-cpu/

```
class Solution {
public:
    vector<int> getOrder(vector<vector<int>>& A) {
        priority_queue<pair<int,int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
        const int n = A.size();
        for (int i = 0; i < n; ++i) A[i].push_back(i);
        sort(A.begin(), A.end());
        long time = 0, num = 0;
        vector<int> res;
        while(num < n || !pq.empty()) {
            if (pq.empty()) time = max(time, (long)A[num][0]);
            while(num < n && time >= A[num][0]) {
                pq.push({A[num][1], A[num][2]});
                ++num;
            }
            auto [pt, index] = pq.top();
            pq.pop();
            res.push_back(index);
            time += pt;
        }
        return res;
    }
};
```
