### 349. Intersection of Two Arrays (Easy)

https://leetcode.com/problems/intersection-of-two-arrays/

```
// Hash table
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> set1(nums1.begin(), nums1.end());
        vector<int> res;
        for (int e : nums2) {
            if (set1.count(e)) {
                res.push_back(e);
                set1.erase(e);
            }
        }          
        return res;
    }
};

// Sort
// Time: O(nlogn)
// Space: O(1)
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        sort(nums1.begin(), nums1.end());
        sort(nums2.begin(), nums2.end());
        vector<int> res;
        res.reserve(nums1.size());
        int i = 0, j = 0;
        while(i < nums1.size() && j < nums2.size()) {
            if (nums1[i] == nums2[j]) {
                if (res.empty() || res.back() != nums1[i]) res.push_back(nums1[i]);
                ++i;
                ++j;
            } 
            else if (nums1[i] < nums2[j]) ++i;
            else ++j;
        }
        return res;
    }
};
```
