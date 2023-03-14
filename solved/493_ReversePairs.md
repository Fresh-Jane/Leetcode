### 493. Reverse Pairs (Hard)

https://leetcode.com/problems/reverse-pairs/

```
// Merge Sort
class Solution {
public:
    int reversePairs(vector<int>& nums) {
        if (nums.size() <= 1) return 0;
        return mergeSort(nums, 0, nums.size());
    }
    int mergeSort(vector<int>& nums, int left, int right) {
        if (left + 1 >= right) return 0;
        int mid = left + (right - left) / 2;
        int res = mergeSort(nums, left, mid) + mergeSort(nums, mid, right);
        vector<int> cache(right-left);
        int j = mid, k = mid;
        int r = 0;
        for (int i = left; i < mid; ++i) {
            while(j < right && (long long)nums[i] > (long long)2 * nums[j]) j++;
            res += j - mid;
            while(k < right && nums[i] > nums[k]) cache[r++] = nums[k++];
            cache[r++] = nums[i];
        }
        move(cache.begin(), cache.begin()+r, nums.begin()+left);
        return res;
    }
};
```
