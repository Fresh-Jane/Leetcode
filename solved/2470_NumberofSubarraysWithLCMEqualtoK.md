### 2470. Number of Subarrays With LCM Equal to K (Medium)

https://leetcode.com/problems/number-of-subarrays-with-lcm-equal-to-k/description/

```
// LCM = a * b / GCD
// LCM: Least common multiple
// GCD: Greatest common divider

// Solution 1
// Given pos i, we count unique LCM values for all subarrays that end at i.
// Time: O(n*d(k)log(k)) 
class Solution {
public:
    long long gcd(long long int a, long long int b) {
        if (b == 0) return a;
        return gcd(b, a % b);
    }
 
    long long lcm(int a, int b) {
        return (a / gcd(a, b)) * b;
    }
    
    int subarrayLCM(vector<int>& nums, int k) {
        int res = 0;
        unordered_map<int, int> m;
        for(int n : nums) {
            unordered_map<int, int> m1;
            if (k % n == 0) {
                ++m[n];
                for (auto& [d, cnt] : m) {
                    m1[lcm(d, n)] += cnt;
                }
                res += m1[k];
            }
            swap(m, m1);
        }
        return res;
    }
};

// Solution 2
// Time: O(n^2)
class Solution {
public:
    long long gcd(long long int a, long long int b) {
        if (b == 0) return a;
        return gcd(b, a % b);
    }
 
    long long lcm(int a, int b) {
        return (a / gcd(a, b)) * b;
    }

    int subarrayLCM(vector<int>& nums, int k) {
        int cnt = 0;
        for(int i = 0; i < nums.size(); i++) {
            for(int j = i, cur = 1; j < nums.size() && k % nums[j] == 0; j++) {
                cur = lcm(cur, nums[j]);
                cnt += cur == k;
            }
        }
        return cnt;
    }
};
```
