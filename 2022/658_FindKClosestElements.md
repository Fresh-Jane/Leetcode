### 658. Find K Closest Elements (Medium)

https://leetcode.com/problems/find-k-closest-elements/

```
// Use BS to find the center two elements closest to x.
// Then use two pointers to find the K closest.
// O(logN + K + KlogK)
class Solution {
public:
    vector<int> findClosestElements(vector<int>& arr, int k, int x) {
        auto it = lower_bound(arr.begin(), arr.end(), x);
        vector<int> res(k);
        auto l = it-1, r = it;
        for (int i = 0; i < k; ++i) {
            if (r == arr.end() || (l >= arr.begin() && abs(*l-x) <= abs(*r-x))) res[i] = *(l--);
            else res[i] = *(r++);
        }
        sort(res.begin(), res.end());
        return res;
    }
};

// Use max_heap priority_queue
// O(NlogK + KlogK)
class Solution {
public:
    vector<int> findClosestElements(vector<int>& arr, int k, int x) {
        auto cmp = [&x](int a, int b) {
            if (abs(a - x) == abs(b - x)) return a < b;
            return abs(a - x) < abs(b - x);
        };
        priority_queue<int, vector<int>, decltype(cmp)> pq(cmp);
        for (int num : arr) {
            pq.push(num);
            if (pq.size() > k) pq.pop();
        }
        vector<int> res;
        res.reserve(k);
        while(!pq.empty()) {
            res.push_back(pq.top());
            pq.pop();
        }
        sort(res.begin(), res.end());
        return res;
    }
}; 
```
