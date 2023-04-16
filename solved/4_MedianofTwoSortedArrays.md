### 4. Median of Two Sorted Arrays (Hard)

https://leetcode.com/problems/median-of-two-sorted-arrays/

```
// Divide and conquer
// Time: O(log(m+n))
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        const int n1 = nums1.size(), n2 = nums2.size();
        if (n1 > n2) return findMedianSortedArrays(nums2, nums1);
        if (n2 == 0) return 0;
        if (n1 == 0) return (n2&1) ? nums2[n2/2] : (nums2[n2/2]+nums2[n2/2-1])*0.5;
        if ((n1+n2)&1) return findK(&nums1[0], n1, &nums2[0], n2, (n1+n2)/2+1);
        return (findK(&nums1[0], n1, &nums2[0], n2, (n1+n2)/2) +
                findK(&nums1[0], n1, &nums2[0], n2, (n1+n2)/2+1)) * 0.5;
    }
    
    double findK(int* nums1, int n1, int* nums2, int n2, int k) {
        if (n1 > n2) return findK(nums2, n2, nums1, n1, k);
        if (n1 == 0) return nums2[k-1];
        if (k == 1) return min(nums1[0], nums2[0]);
        int k1 = min(n1, k/2), k2 = k-k1;
        if (nums1[k1-1] < nums2[k2-1]) return findK(nums1+k1, n1-k1, nums2, n2, k-k1);
        else return findK(nums1, n1, nums2+k2, n2-k2, k-k2);
    }
};

```
