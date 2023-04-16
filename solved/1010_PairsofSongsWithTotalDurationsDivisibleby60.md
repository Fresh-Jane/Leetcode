### 1010. Pairs of Songs With Total Durations Divisible by 60 (Medium)

https://leetcode.com/problems/pairs-of-songs-with-total-durations-divisible-by-60/description/

```
// One pass
class Solution {
public:
    int numPairsDivisibleBy60(vector<int>& time) {
        vector<int> res_map(60, 0);
        int res = 0; 
        for (int t : time) {
            const int remain = t % 60;
            if (remain == 0) res += res_map[0];
            else res += res_map[60 - remain];
            res_map[remain]++;
        }
        return res;
    }
};

// Two pass
// Time: O(N), Space: O(N)
class Solution {
public:
    int numPairsDivisibleBy60(vector<int>& time) {
        vector<int> res_map(60, 0);
        for (int t : time) res_map[t % 60]++;
        long long res = 0;
        for (int i = 0; i <= 30; ++i) {
            if (i == 30 || i == 0) res += 0.5 * res_map[i] * (res_map[i] - 1);
            else res += res_map[i] * res_map[60-i];
        }
        return res;
    }
};
```
