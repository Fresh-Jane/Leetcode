### 315. Count of Smaller Numbers After Self (Hard)

https://leetcode.com/problems/count-of-smaller-numbers-after-self/

```
// Merge sort
// Use vector index to keep if i < j, nums[index[i]] < nums[index[j]].
class Solution {
public:
    vector<int> countSmaller(vector<int>& nums) {
        const int n = nums.size();
        vector<int> index(n, 0), res(n, 0);
        iota(index.begin(), index.end(), 0);
        mergeSort(nums, 0, n, index, res);
        return res;
    }
    void mergeSort(vector<int>& nums, int left, int right, vector<int>& index, vector<int>& res) {
        if (left + 1 >= right) return;
        int mid = left + (right - left) / 2;
        mergeSort(nums, left, mid, index, res);
        mergeSort(nums, mid, right, index, res);
        vector<int> cache(right-left);
        int j = mid, k = 0;
        int count = 0;
        for(int i = left; i < mid; ++i) {
            while(j < right && nums[index[i]] > nums[index[j]]) {
                count++;
                cache[k++] = index[j++];
            }
            cache[k++] = index[i];
            res[index[i]] += count;
        }
        move(cache.begin(), cache.begin()+k, index.begin()+left);
    }
};
```
