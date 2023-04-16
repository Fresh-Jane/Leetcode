### 1207. Unique Number of Occurrences (Easy)

https://leetcode.com/problems/unique-number-of-occurrences/description/

```
class Solution {
public:
    bool uniqueOccurrences(vector<int>& arr) {
        unordered_map<int, int> cnt;
        for (const int v : arr) cnt[v]++;
        unordered_set<int> res;
        for (const auto& pair : cnt) {
            if (res.count(pair.second)) return false;
            res.insert(pair.second);
        }
        return true;
    }
};
```
