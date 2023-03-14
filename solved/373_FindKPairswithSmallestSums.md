### 373. Find K Pairs with Smallest Sums (Medium)

https://leetcode.com/problems/find-k-pairs-with-smallest-sums/

```
class Solution {
public:
    vector<vector<int>> kSmallestPairs(vector<int>& nums1, vector<int>& nums2, int k) {
        const int n1 = nums1.size(), n2 = nums2.size();
        using S = pair<int,int>;
        auto cmp = [&nums1, &nums2](const S& p1, const S& p2){
            return nums1[p1.first] + nums2[p1.second] > nums1[p2.first] + nums2[p2.second];
        };
        priority_queue<S, vector<S>, decltype(cmp)> pq(cmp);
        pq.push({0, 0});
        vector<vector<int>> res;
        while(k-- && !pq.empty()) {
            auto [x, y] = pq.top(); pq.pop();
            res.push_back({nums1[x], nums2[y]});
            if (y + 1 < n2) pq.push({x, y + 1});
            if (y == 0 && x + 1 < n1) pq.push({x + 1, y});
        }
        return res;
    }
};
```
