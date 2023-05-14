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

// Heap sort
// Time: O(nlogn)
// Space: O(logn) 
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        heapSort(nums);
        return nums;
    }

    void heapSort(vector<int>& nums) {
        const int n = nums.size();
        for (int i = n / 2 - 1; i >= 0; --i) {
            heapify(nums, n, i);
        }
        for (int i = n - 1; i >= 0; --i) {
            swap(nums[i], nums[0]);
            heapify(nums, i, 0);
        }
    }

    void heapify(vector<int>& nums, int n, int i) {
        int largest = i;
        int left = 2 * i + 1;
        int right = 2 * i + 2;

        if (left < n && nums[left] > nums[largest]) {
            largest = left;
        }
        if (right < n && nums[right] > nums[largest]) {
            largest = right;
        }
        if (largest != i) {
            swap(nums[i], nums[largest]);
            heapify(nums, n, largest);
        }
    }
};
```
