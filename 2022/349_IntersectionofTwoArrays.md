### 349. Intersection of Two Arrays (Easy)

https://leetcode.com/problems/intersection-of-two-arrays/

```
// Sort
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        sort(nums1.begin(), nums1.end());
        sort(nums2.begin(), nums2.end());
        const int n1 = nums1.size(), n2 = nums2.size();
        vector<int> res;
        int i = 0, j = 0;
        while(i < n1 && j < n2) {
            if (nums1[i] == nums2[j]) {
                if (res.empty() || nums1[i] != res.back()) res.push_back(nums1[i]);
                ++i;
                ++j;
            } else if (nums1[i] < nums2[j]) ++i;
            else ++j;
        }
        return res;
    }
};

// Hashmap
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set set1(nums1.begin(), nums1.end());
        unordered_set set2(nums2.begin(), nums2.end());
        vector<int> res;
        for (int num : set1) 
            if (set2.count(num)) res.push_back(num);
        return res;
    }
};
```
