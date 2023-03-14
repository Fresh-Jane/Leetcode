### 2447. Number of Subarrays With GCD Equal to K (Medium)

https://leetcode.com/problems/number-of-subarrays-with-gcd-equal-to-k/description/

```
class Solution {
public:
    int subarrayGCD(vector<int>& nums, int k) {
        int res = 0;
        unordered_map<int, int> m;
        for (int n : nums) {
            unordered_map<int, int> m1;
            if (n % k == 0) {
                ++m[n];
                for (auto& [d, cnt] : m) {
                    m1[__gcd(d, n)] += cnt;
                }
                res += m1[k];
            }
            swap(m, m1);
        }
        return res;
    }
};
```
