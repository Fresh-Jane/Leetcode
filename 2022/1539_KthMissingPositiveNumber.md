### 1539. Kth Missing Positive Number (Easy)

https://leetcode.com/problems/kth-missing-positive-number/

```
// Brute force
// Time: O(N)
class Solution {
public:
    int findKthPositive(vector<int>& arr, int k) {
        const int n = arr.size();
        int i = 1, j = 0;
        while(j < n && k) {
            if (arr[j] == i) {
                ++i;
                ++j;
            } else if (arr[j] > i) {
                --k;
                if (k == 0) return i;
                ++i;
            }
            else ++j;
            
        }
        return i + k - 1;
    }
};

// Binary search
// arr[i] = i+k+1
class Solution {
public:
    int findKthPositive(vector<int>& arr, int k) {
        int l = 0, r = arr.size();
        while(l < r) {
            int m = l + (r - l) / 2;
            if (arr[m]-1-m < k) l = m+1;
            else r = m;
        }
        return l + k;
    }
};
```
