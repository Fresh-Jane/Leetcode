### 2007. Find Original Array From Doubled Array (Medium)

https://leetcode.com/problems/find-original-array-from-doubled-array/

```
class Solution {
public:
    vector<int> findOriginalArray(vector<int>& changed) {
        if (changed.size() % 2) return {};
        map<int, int> s;
        for (int i : changed) s[i]++; 
        vector<int> res;
        for (auto p : s) {
            if (p.second == 0) continue;
            const int cur = p.first, change = 2*cur, cur_cnt = p.second;
            if (cur == change) {
                if (cur_cnt % 2) return {};
                for (int i = 0; i < cur_cnt / 2; ++i) res.push_back(cur);
            } else{
                if (!s.count(change) || s[change] < cur_cnt) return {};
                for (int i = 0; i < cur_cnt; ++i) res.push_back(cur);
                s[cur] = 0;
                s[change] -= cur_cnt;
            }
        }
        return res;
    }
};
```
