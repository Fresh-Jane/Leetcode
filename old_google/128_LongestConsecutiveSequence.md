### 128. Longest Consecutive Sequence (Medium)

https://leetcode.com/problems/longest-consecutive-sequence/

```
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        unordered_map<int, int> map;
        for (const int num : nums) map[num] = 1;
        int res = 0;
        for (const int num : nums) {
            if (map[num] == -1) continue;
            int l = 0;
            while (map.count(num - l)) {
                map[num - l] = -1;
                ++l;
            }
            int r = 1;
            while (map.count(num + r)) {
                map[num + r] = -1;
                ++r;
            }
            res = max(res, l + r - 1);
        }
        return res;
    }
};
```
