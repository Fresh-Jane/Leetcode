### 992. Subarrays with K Different Integers (Hard)

https://leetcode.com/problems/subarrays-with-k-different-integers/

```
// SLiding window
//Solution1:  https://leetcode.com/problems/subarrays-with-k-different-integers/discuss/523136/JavaC%2B%2BPython-Sliding-Window
class Solution {
public:
    int subarraysWithKDistinct(vector<int>& nums, int k) {
        return atMostK(nums, k) - atMostK(nums, k - 1);
    }
    int atMostK(const vector<int>& nums, int k) {
        int i = 0, res = 0;
        unordered_map<int, int> cnt;
        for (int j = 0; j < nums.size(); ++j) {
            if (!cnt[nums[j]]++) k--;
            while(k < 0) {
                if (!--cnt[nums[i]]) k++;
                i++;
            }
            res += j - i + 1;
        }
        return res;
    }
};

// Solution2: https://leetcode.com/problems/subarrays-with-k-different-integers/discuss/235235/C%2B%2BJava-with-picture-prefixed-sliding-window
class Solution {
public:
    int subarraysWithKDistinct(vector<int>& A, int K) {
        int res = 0;
        vector<int> m(A.size() + 1);
        for(int i = 0, j = 0, prefix = 0, cnt = 0; i < A.size(); ++i) {
            if (!m[A[i]]++) ++cnt;
            if (cnt > K) {
                --m[A[j++]];
                --cnt;
                prefix = 0;
            }
            while (m[A[j]] > 1) {
                ++prefix;
                --m[A[j++]];
            }
            if (cnt == K) res += prefix + 1;
        }
        return res;
    }
};
```
