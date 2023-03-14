### 57. Insert Interval (Medium)

https://leetcode.com/problems/insert-interval/

```
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& oi, vector<int>& ni) {
        const int n = oi.size();
        vector<vector<int>> res;
        int i = 0;
        for (; i < n; ++i) {
            if (oi[i][0] > ni[1]) break;
            else if (oi[i][1] < ni[0]) res.push_back(oi[i]);
            else {
                ni[0] = min(oi[i][0], ni[0]);
                ni[1] = max(oi[i][1], ni[1]);
            }
        }
        res.push_back(ni);
        while(i < n) res.push_back(oi[i++]);
        return res;
    }
};
```
