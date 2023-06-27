### 852. Peak Index in a Mountain Array (Medium)

https://leetcode.com/problems/peak-index-in-a-mountain-array/description/

```
class Solution {
public:
    int peakIndexInMountainArray(vector<int>& arr) {
        int l = 0, r = arr.size() - 1;
        while(l < r) {
            int m = l + (r - l) / 2;
            if (arr[m] < arr[m+1]) l = m + 1;
            else r = m;
        }
        return l;
    }
};
```
