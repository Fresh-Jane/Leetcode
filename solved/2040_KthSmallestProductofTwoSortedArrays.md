### 2040. Kth Smallest Product of Two Sorted Arrays (Hard)

https://leetcode.com/problems/kth-smallest-product-of-two-sorted-arrays/

```
class Solution {
public:
    long long kthSmallestProduct(vector<int>& nums1, vector<int>& nums2, long long k) {
        auto it1 = lower_bound(nums1.begin(), nums1.end(), 0);
        auto it2 = lower_bound(nums2.begin(), nums2.end(), 0);
        vector<long long> neg1(it1-nums1.begin()), pos1(it1, nums1.end());
        for (auto it = nums1.begin(); it < it1; ++it) neg1[it1-it-1] = -(*it);
        vector<long long> neg2(it2-nums2.begin()), pos2(it2, nums2.end());
        for (auto it = nums2.begin(); it < it2; ++it) neg2[it2-it-1] = -(*it);
        long long negcnt = neg1.size() * pos2.size() + neg2.size() * pos1.size();
        bool is_neg;
        if (k > negcnt) {
            k -= negcnt;
            is_neg = false;
        } else {
            k = negcnt - k + 1;
            vector<long long> tmp = neg2;
            neg2 = pos2;
            pos2 = tmp;
            is_neg = true;
        }
        
        long long l = 0, r = 1e10;
        while(l < r) {
            long long m = l + (r - l) / 2;
            if (count(neg1, neg2, m) + count(pos1, pos2, m) >= k) r = m;
            else l = m + 1;
        }
        return is_neg ? -l : l;
    }
    
    long long count(vector<long long>& arr1, vector<long long>& arr2, long long m) {
        long long res = 0, j = arr2.size() - 1;
        for (int i = 0; i < arr1.size(); ++i) {
            while(j >= 0 && arr1[i] * arr2[j] > m) --j;
            res += j + 1;
        }
        return res;
    }
};
```
