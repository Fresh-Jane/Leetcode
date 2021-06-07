### 215. Kth Largest Element in an Array (Medium)

https://leetcode.com/problems/kth-largest-element-in-an-array/

```
// Use priority_queue, max heap
// Time: O(nlogk)
class Solution1 {
public:
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int, vector<int>, std::greater<int>> q;
        for (const int n : nums) {
            q.push(n);
            if (q.size() > k) q.pop();
        }
        return q.top();
    }
};

class Solution2 {
public:
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int> pq(nums.begin(), nums.end());
        for (int i = 0; i < k - 1; i++)
            pq.pop(); 
        return pq.top();
    }
};
```
