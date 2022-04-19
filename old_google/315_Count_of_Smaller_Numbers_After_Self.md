### 315. Count of Smaller Numbers After Self (Hard)

https://leetcode.com/problems/count-of-smaller-numbers-after-self/

```
https://leetcode.com/problems/count-of-smaller-numbers-after-self/discuss/76607/C%2B%2B-O(nlogn)-Time-O(n)-Space-MergeSort-Solution-with-Detail-Explanation
Merge sort based reverse pair number calculate.

Time: O(NLogN)
Space: O(N)

class Solution {
public:
    void merge_sort(const vector<int>& nums, int s, int t, vector<int>& res, vector<int>& index) {
        if (t - s <= 1) return;
        int m = s + (t - s) / 2;
        merge_sort(nums, s, m, res, index);
        merge_sort(nums, m, t, res, index);
        vector<int> tmp;
        tmp.reserve(t - s);
        int j = m;
        for (int i = s; i < m; ++i) {
            while(j < t && nums[index[i]] > nums[index[j]]) 
                tmp.push_back(index[j++]);
            tmp.push_back(index[i]);
            res[index[i]] += j - m;
        }
        move(tmp.begin(), tmp.end(), index.begin()+s);
    }
    
    vector<int> countSmaller(vector<int>& nums) {
        const int n = nums.size();
        vector<int> res(n, 0), index(n, 0);
        iota(index.begin(), index.end(), 0);
        merge_sort(nums, 0, n, res, index);
        return res;
    }
};
```
