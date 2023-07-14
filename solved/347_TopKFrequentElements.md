### 347. Top K Frequent Elements (Medium)

https://leetcode.com/problems/top-k-frequent-elements/description/

```
// priority queue
// Time: O(NlogK)
class Solution {
public:
    struct Cmp {
        bool operator() (const pair<int, int>& p1, const pair<int, int>& p2) {
            return p1.first > p2.first;
        }
    };
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> cnt_m;
        for (int num : nums) cnt_m[num]++;
        priority_queue<pair<int, int>, vector<pair<int, int>>, Cmp> pq;
        for (const auto& cnt_pair : cnt_m) {
            pq.push({cnt_pair.second, cnt_pair.first});
            if (pq.size() > k) pq.pop();
        }
        vector<int> res;
        while(!pq.empty()) {
            res.push_back(pq.top().second);
            pq.pop();
        }
        return res;
    }
};

// bucket sort
// Time: O(N)
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> cnt_m;
        for (int num : nums) cnt_m[num]++;
        const int n = nums.size();
        vector<vector<int>> bucket(n+1);
        for (const auto& cnt : cnt_m) bucket[cnt.second].push_back(cnt.first);
        vector<int> res;
        for (int i = n; i >= 0; --i) {
            if (res.size() == k) break;
            if (!bucket[i].empty()) {
                for (int num : bucket[i]) {
                    res.push_back(num);
                    if (res.size() == k) break;
                }
            }
        }
        return res;
    }
};
```
