### 1762. Buildings With an Ocean View (Medium)

https://leetcode.com/problems/buildings-with-an-ocean-view/

```
class Solution {
public:
    vector<int> findBuildings(vector<int>& heights) {
        vector<int> res;
        int max_h = 0;
        for (int i = heights.size() - 1; i >= 0; --i) {
            if (heights[i] > max_h) res.push_back(i);
            max_h = max(max_h, heights[i]);
        }
        reverse(res.begin(), res.end());
        return res;
    }
};
```
