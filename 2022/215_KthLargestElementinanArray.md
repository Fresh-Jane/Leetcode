### 215. Kth Largest Element in an Array (Medium)

https://leetcode.com/problems/kth-largest-element-in-an-array/

```
// min_heap
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int, vector<int>, greater<int>> pq;
        for (int num : nums) {
            pq.push(num);
            if (pq.size() > k) pq.pop();
        }
        return pq.top();
    }
};

// QuickSelect
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        int left = 0, right = nums.size() - 1, kth;
        int index = nums.size() - k;
        while(true) {
            int p = partition(nums, left, right);
            if (p == index) {
                kth = nums[p];
                break;
            }
            if (p < index) left = p + 1;
            else right = p - 1;
        }
        return kth;
    }
private:
    int partition(vector<int>& nums, int left, int right) {
        int pivot = nums[left], l = left + 1, r = right;
        while(l <= r) {
            while(l <= r && nums[l] <= pivot) l++;
            while(l <= r && nums[r] >= pivot) r--;
            if (l <= r) swap(nums[l++], nums[r--]);
        }
        swap(nums[left], nums[r]);
        return r;
    }
};
```
