### 378. Kth Smallest Element in a Sorted Matrix (Medium)

https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/

```
class Solution {
public:
    int kthSmallest(vector<vector<int>>& matrix, int k) {
        const int n = matrix.size();
        using S = tuple<int, int, int>;
        priority_queue<S, vector<S>, greater<S>> pq;
        pq.push({matrix[0][0], 0, 0});
        int res = 0;
        while(k-- && !pq.empty()) {
            auto [val, i, j] = pq.top(); pq.pop();
            res = val;
            if (j + 1 < n) pq.push({matrix[i][j+1], i, j+1});
            if (j == 0 && i + 1 < n) pq.push({matrix[i+1][j], i+1, j}); // avoid redundant
        }
        return res;
    }
};
```
