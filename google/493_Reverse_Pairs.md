### 493. Reverse Pairs (Hard)

https://leetcode.com/problems/reverse-pairs/

```
Merge sort based

class Solution {
public:
    int count;
    void check_num(vector<int>& nums, int s, int m, int t) {
        int l = s, r = m + 1;
        while(l <= m && r <= t) {
            if ((long)nums[l] > (long)2 * nums[r]) {
                count += (m - l) + 1;
                r++;
            } else {
                l++;
            }
        }
        sort(nums.begin()+s, nums.begin()+t+1);
    }
    
    void merge_sort(vector<int>& nums, int s, int t) {
        if (s == t) return;
        int m = (s + t) / 2;
        merge_sort(nums, s, m);
        merge_sort(nums, m+1, t);
        check_num(nums, s, m, t);
    }
    
    int reversePairs(vector<int>& nums) {
        const int n = nums.size();
        count = 0;
        merge_sort(nums, 0, n-1);
        return count;
    }
};
```
