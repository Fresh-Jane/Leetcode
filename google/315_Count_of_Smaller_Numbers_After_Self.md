### 315. Count of Smaller Numbers After Self (Hard)

https://leetcode.com/problems/count-of-smaller-numbers-after-self/

```
https://leetcode.com/problems/count-of-smaller-numbers-after-self/discuss/76607/C%2B%2B-O(nlogn)-Time-O(n)-Space-MergeSort-Solution-with-Detail-Explanation
Merge sort based reverse pair number calculate.

Time: O(NLogN)
Space: O(N)

class Solution {
public:
    void merge_sort(const vector<int>& nums, vector<int>& index, vector<int>& res, int l, int r) {
        int count = r - l;
        if (count > 1) {
            int step = count / 2;
            int m = l + step;
            merge_sort(nums, index, res, l, m);
            merge_sort(nums, index, res, m, r);
            vector<int> tmp;
            tmp.reserve(count);
            int idx1 = l;
            int idx2 = m;
            int reverse_num = 0;
            while(idx1 < m || idx2 < r) {
                if (idx2 == r ||
                    (idx1 < m && nums[index[idx1]] <= nums[index[idx2]])) {
                    tmp.push_back(index[idx1]);
                    res[index[idx1]] += reverse_num;
                    idx1++;
                } else {
                    tmp.push_back(index[idx2]);
                    reverse_num++;
                    idx2++;
                }
            }
            move(tmp.begin(), tmp.end(), index.begin()+l);
        }
    }
    
    vector<int> countSmaller(vector<int>& nums) {
        const int n = nums.size();
        vector<int> res(n, 0);
        vector<int> index(n, 0);
        iota(index.begin(), index.end(), 0);
        merge_sort(nums, index, res, 0, n);
        return res;
    }
};
```
