### 2007. Find Original Array From Doubled Array (Medium)

https://leetcode.com/problems/find-original-array-from-doubled-array/

```
// Time: O(N+klogk)
class Solution {
public:
    vector<int> findOriginalArray(vector<int>& changed) {
        if (changed.size() % 2) return {};
        map<int, int> cnt;
        for (const int c : changed) cnt[c]++;
        if (cnt.find(0) != cnt.end() && cnt[0] % 2 != 0) return {};
        vector<int> res;
        for (auto& pair : cnt) {
            if (pair.second == 0) continue;
            const int x = pair.first, x2 = pair.first * 2;
            if (cnt.find(x2) == cnt.end() || pair.second > cnt[x2]) return {};
            while (cnt[x] > 0) {
                res.push_back(x);
                cnt[x]--;
                cnt[x2]--;
            }
        }
        return res;
    }
};
```
