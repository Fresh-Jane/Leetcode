### 912. Sort an Array (Medium)

https://leetcode.com/problems/sort-an-array/

```
// merge sort
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        mergeSort(nums, 0, nums.size());
        return nums;
    }
    void mergeSort(vector<int>& nums, int left, int right) {
        if (left < right-1) {
            int mid = left + (right - left)/2;
            mergeSort(nums, left, mid);
            mergeSort(nums, mid, right);
            merge(nums, left, mid, right);
        }
    }
    void merge(vector<int>& nums, int left, int mid, int right) {
        vector<int> lnum(nums.begin()+left, nums.begin()+mid);
        vector<int> rnum(nums.begin()+mid, nums.begin()+right);
        int ln = mid - left, rn = right - mid;
        int i = 0, j = 0, k = left;
        while(i < ln && j < rn) {
            if (lnum[i] < rnum[j]) nums[k++] = lnum[i++];
            else nums[k++] = rnum[j++];
        }
        while(i < ln) nums[k++] = lnum[i++];
        while(j < rn) nums[k++] = rnum[j++];
    }
};
```
