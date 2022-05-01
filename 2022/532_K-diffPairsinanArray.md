### 532. K-diff Pairs in an Array (Medium)

https://leetcode.com/problems/k-diff-pairs-in-an-array/

```
// Sort and binary search
class Solution {
public:
    int findPairs(vector<int>& nums, int k) {
        sort(nums.begin(), nums.end());
        const int n = nums.size();
        int res = 0;
        for (int i = 0; i < n; ++i) {
            if (i > 0 && nums[i] == nums[i-1]) continue;
            if (binary_search(nums.begin()+i+1, nums.end(), nums[i]+k)) ++res;
        }
        return res;
    }
};

// hashmap
class Solution {
public:
    int findPairs(vector<int>& nums, int k) {
        if (nums.size() <= 1) return 0;
        int res = 0;
        unordered_map<int, int> m;
        for (int num : nums) m[num]++;
        for (auto p : m) {
            if (k == 0) res += p.second >= 2 ? 1 : 0;
            else res += m.count(p.first+k);
        }
        return res;
    }
};
```
